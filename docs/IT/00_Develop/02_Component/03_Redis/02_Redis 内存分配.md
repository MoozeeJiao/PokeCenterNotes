> 出处：https://www.liuyushuai.com/blog/z8WXA8XPApdj

redis 没有直接用 C语言提供的内存管理，而是做了一个可管理已分配内存大小以及添加自己策略的实现。

例如 [[01_Redis String 实现 |SDS]] 内存管理函数定义如下：

``` C++
#include "zmalloc.h" 
#define s_malloc zmalloc 
#define s_realloc zrealloc 
#define s_free zfree
```

其中 zmalloc zrealloc zfree 会根据不同的编译参数使用具体的内存管理库。

``` C++
#if defined(USE_TCMALLOC) 
#define ZMALLOC_LIB ("tcmalloc-" __xstr(TC_VERSION_MAJOR) "." __xstr(TC_VERSION_MINOR)) 
#include <google/tcmalloc.h> 
#if (TC_VERSION_MAJOR == 1 && TC_VERSION_MINOR >= 6) || (TC_VERSION_MAJOR > 1) 
#define HAVE_MALLOC_SIZE 1 
#define zmalloc_size(p) tc_malloc_size(p) 
#else 
#error "Newer version of tcmalloc required" 
#endif 

#elif defined(USE_JEMALLOC) 
#define ZMALLOC_LIB ("jemalloc-" __xstr(JEMALLOC_VERSION_MAJOR) "." __xstr(JEMALLOC_VERSION_MINOR) "." __xstr(JEMALLOC_VERSION_BUGFIX)) 
#include <jemalloc/jemalloc.h> 
#if (JEMALLOC_VERSION_MAJOR == 2 && JEMALLOC_VERSION_MINOR >= 1) || (JEMALLOC_VERSION_MAJOR > 2) 
#define HAVE_MALLOC_SIZE 1 
#define zmalloc_size(p) je_malloc_usable_size(p) 
#else 
#error "Newer version of jemalloc required" 
#endif 

#elif defined(__APPLE__) 
#include <malloc/malloc.h> 
#define HAVE_MALLOC_SIZE 1 
#define zmalloc_size(p) malloc_size(p) 
#endif 

#ifndef ZMALLOC_LIB 
#define ZMALLOC_LIB "libc" 
#ifdef __GLIBC__ 
#include <malloc.h> 
#define HAVE_MALLOC_SIZE 1 
#define zmalloc_size(p) malloc_usable_size(p) 
#endif 
#endif
```

redis 会根据平台和依赖库来决定内存分配方案，libc是c语言默认内存管理库，但是碎片率较高，其他3个在这方面做了优化。linux下默认使用 jemalloc。

* google/tcmalloc
* jemalloc/jemalloc
* malloc/malloc
* libc

主要看一下 zmalloc 的实现：

``` C++
void *zmalloc(size_t size) { 
	void *ptr = malloc(size+PREFIX_SIZE); 
	if (!ptr) zmalloc_oom_handler(size); 
#ifdef HAVE_MALLOC_SIZE 
	update_zmalloc_stat_alloc(zmalloc_size(ptr)); 
	return ptr; 
#else 
	*((size_t*)ptr) = size; 
	update_zmalloc_stat_alloc(size+PREFIX_SIZE); 
	return (char*)ptr+PREFIX_SIZE; 
#endif 
}
```

根据 HAVE_MALLOC_SIZE 是否定义有两个分支，常量表示是否记录分配内存大小。除了 libc其他三个库都提供了获取内存占用函数。libc的由redis自己实现，就是在申请内存的时候在头部多申请一块 PREFIX_SIZE 的空间用来保存。：

``` C++
size_t zmalloc_size(void *ptr) {
	void *realptr = (char*)ptr-PREFIX_SIZE; 
	size_t size = *((size_t*)realptr); 
	/* Assume at least that all the allocations are padded at sizeof(long) by 
	* the underlying allocator. */ 
	if (size&(sizeof(long)-1)) 
		size += sizeof(long)-(size&(sizeof(long)-1)); 
	return size+PREFIX_SIZE; }
```