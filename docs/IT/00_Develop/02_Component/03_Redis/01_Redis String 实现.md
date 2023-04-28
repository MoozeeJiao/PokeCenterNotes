> 转译自： https://www.sobyte.net/post/2022-04/redis-string/
> 原博：https://www.luozhiyun.com/archives/663

# Simple Dynamic String

SDS 实现在 sds.c 和 sds.h 两个文件中。其数据结构包含 header 和 data 两部分。其中 header 又包含以下 3 领域：
* len：表示 data 的长度；
* alloc：表示已分配的内存；
* flags：表示 sds 的数据类型。

早期版本中，header 固定为 8 字节，所以较小的字符串会有浪费。sds 2.0 之后的新版本中，header 的长度将会根据输入字符串的长度进行调整。且为了防止编译器对结构体进行字节对齐，使用了\_\_attribute\_\_ ((\_\_packed\_\_))关键字来让结构体紧凑排列。

现共有 5 种header：

``` C++
struct __attribute__ ((__packed__)) sdshdr8 { // 占用 3 byte 
	uint8_t len; /* used */ 
	uint8_t alloc; /* excluding the header and null terminator */ 
	unsigned char flags; /* 3 lsb of type, 5 unused bits */ 
	char buf[]; 
}; 
struct __attribute__ ((__packed__)) sdshdr16 { // 占用 5 byte 
	uint16_t len; /* used */ 
	uint16_t alloc; /* excluding the header and null terminator */ 
	unsigned char flags; /* 3 lsb of type, 5 unused bits */ 
	char buf[]; 
}; 
struct __attribute__ ((__packed__)) sdshdr32 { // 占用 9 byte 
	uint32_t len; /* used */ 
	uint32_t alloc; /* excluding the header and null terminator */ 
	unsigned char flags; /* 3 lsb of type, 5 unused bits */ 
	char buf[]; 
}; 
struct __attribute__ ((__packed__)) sdshdr64 { // 占用 17 byte 
	uint64_t len; /* used */ 
	uint64_t alloc; /* excluding the header and null terminator */ 
	unsigned char flags; /* 3 lsb of type, 5 unused bits */ 
	char buf[]; 
};
```

## sdsnewlen

sds 的主要构建函数为：

``` C++
sds sdsnewlen(const void *init, size_t initlen)
```

入参为 C 中的字符串和所需要创建的的长度，其他创建函数都最终调用 sdsnewlen 函数。

创建一个 string 对象主要有 3 步：申请空间；构造结构体；拷贝入字符串。下面是 sdsnewlen 的实现：

### 1、申请内存空间

``` C++
sds sdsnewlen(const void *init, size_t initlen) { 
	void *sh; //指向SDS结构体的指针 
	sds s; //sds类型变量，即char*字符数组 
	char type = sdsReqType(initlen); //根据数据大小获取sds header 类型 
	if (type == SDS_TYPE_5 && initlen == 0) 
		type = SDS_TYPE_8; 
	int hdrlen = sdsHdrSize(type); // 根据类型获取sds header大小 
	unsigned char *fp; /* flags pointer. */ 
	assert(hdrlen+initlen+1 > initlen); /* Catch size_t overflow */ 
	sh = s_malloc(hdrlen+initlen+1); //新建SDS结构，并分配内存空间，这里加1是因为需要在最后加上\0 
	... 
	return s; 
}
```

可以看到，首先用 sdsReqType 函数来确定指定长度字符串需要用哪一种 header，接着用 sdsHdrSize 获取 header 长度，总共需要申请 hreader 长度 + 指定长度 + 1 （'\\0'）的空间。这里对长度进行了溢出保护。

``` C++
static inline char sdsReqType(size_t string_size) { 
	if (string_size < 1<<5) // 小于 32 
		return SDS_TYPE_5; 
	if (string_size < 1<<8) // 小于 256 
		return SDS_TYPE_8; 
	if (string_size < 1<<16) // 小于 65,536 
		return SDS_TYPE_16; 
#if (LONG_MAX == LLONG_MAX) 
	if (string_size < 1ll<<32) 
		return SDS_TYPE_32; 
	return SDS_TYPE_64; 
#else 
	return SDS_TYPE_32; 
#endif 
}
```

其中 \#if \#endif 指令控制源文件的编译，32位系统 long 4 字节，64位系统 long 8 字节， long long 都是 8 字节。所以32位系统最多只能用到 SDS_TYPE_32。

### 2、构造结构体

先申请一块头结构内存，再初始化头结构指针指向位置。

``` C++
#define SDS_HDR_VAR(T, s) struct sdshdr##T *sh = (void*)((s)-(sizeof(struct sdshdr##T)));

sds sdsnewlen(cosnt void *init, size_t initlen) {
	...
	sh = s_malloc(hdrlen+initlen+1); //1.申请内存
	if (sh == NULL) return NULL;
	if (init==SDS_NOINIT)
		init = NULL;
	else if (!init)
		memset(sh, 0, hdrlen+initlen+1);//2.将内存都设置为0
	s = (char*)sh+hdrlen;//3.将s指针执行数据起始位置
	fp = ((unsigned char*)s)-1;//4.将fp指针指向sds header的flags字段
	switch(type) {
		case SDS_TYPE_5: {
			*fp = type | (initlen << SDS_TYPE_BITS);//SDS_TYPE_BITS=3
			break;
		}
		case SDS_TYPE_8: {
			SDS_HDR_VAR(8,s); //5.构造header
			sh->len = initlen; //初始化header
			sh->alloc = initlen;
			*fp = type;
			break;
		}
		...
	}
	...
	return s;
}
```

### 3、字符串拷贝

``` C++
sds sdsnewlen(const void *init, size_t initlen) {
    ...
    if (initlen && init)  
        memcpy(s, init, initlen); //将要传入的字符串拷贝给sds变量s
    s[initlen] = '\0'; //变量s末尾增加\0，表示字符串结束
    return s;
}
```

## sdscatlen

``` C++
sds sdscatlen(sds s, const void *t, size_t len) {
    size_t curlen = sdslen(s); // 获取字符串 len 大小
    //根据要追加的长度len和目标字符串s的现有长度，判断是否要增加新的空间
    //返回的还是字符串起始内存地址
    s = sdsMakeRoomFor(s,len);
    if (s == NULL) return NULL;
    // 将新追加的字符串拷贝到末尾
    memcpy(s+curlen, t, len);
    // 重新设置字符串长度
    sdssetlen(s, curlen+len);
    s[curlen+len] = '\0';
    return s;
}
```

字符串追加函数里，主要是调用了 sdsMakeRoomFor 函数，主要做的是：

1. 有没有足够的剩余空间，有的话直接返回；
2. 没有剩余空间，需要扩容，扩容多少？
3. 是否可以在原来的位置追加，还是申请一块新内存？

### 扩容

``` C++
sds sdsMakeRoomFor(sds s, size_t addlen) {
    void *sh, *newsh;
    size_t avail = sdsavail(s); //这里是用 alloc-len,表示可用资源
    size_t len, newlen;
    char type, oldtype = s[-1] & SDS_TYPE_MASK;
    int hdrlen;

    if (avail >= addlen) return s; // 如果有空间剩余，那么直接返回

    len = sdslen(s); // 获取字符串 len 长度
    sh = (char*)s-sdsHdrSize(oldtype); //获取到header的指针
    newlen = (len+addlen); // 新的内存空间
    if (newlen < SDS_MAX_PREALLOC) //如果小于 1m， 那么存储空间直接翻倍
        newlen *= 2;
    else
        newlen += SDS_MAX_PREALLOC; //超过了1m，那么只会多增加1m空间
    ...
    return s;
}
```

使用 alloc-len 判断是否有剩余空间，如果不够会扩容，如果 len+addlen 小于 1m，那么新空间会翻倍 (len+addlen)\*2，否则多增加 1m (len+addlen)+1m。

### 内存申请

``` C++
sds sdsMakeRoomFor(sds s, size_t addlen) {
    ...

    type = sdsReqType(newlen); // 根据新的空间占用计算 sds 类型 

    hdrlen = sdsHdrSize(type); // header 长度
    if (oldtype==type) { // 和原来header一样，那么可以复用原来的空间
        newsh = s_realloc(sh, hdrlen+newlen+1); // 申请一块内存，并追加大小
        if (newsh == NULL) return NULL;
        s = (char*)newsh+hdrlen;
    } else { 
        //如果header 类型变了，表示内存头变了，那么需要重新申请内存
        //因为如果使用s_realloc只会向后追加内存
        newsh = s_malloc(hdrlen+newlen+1);
        if (newsh == NULL) return NULL;
        memcpy((char*)newsh+hdrlen, s, len+1);
        s_free(sh); // 释放掉原内存
        s = (char*)newsh+hdrlen;
        s[-1] = type;
        sdssetlen(s, len);
    }
    sdssetalloc(s, newlen);//重新设置alloc字段
    return s;
}
```

如果 header 的类型没有变，则利用 realloc 在原有内存后面追加区域。header 变大了就只能申请一块新内存。