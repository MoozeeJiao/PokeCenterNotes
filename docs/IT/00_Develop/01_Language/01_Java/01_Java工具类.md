# Java集合类

## Set

### Navigable接口

SortedMap接口的扩展lowerEntry、floorEntry、ceilingEntry 和 higherEntry 分别返回小于、小于等于、大于等于、大于给定元素的元素，如果不存在这样的元素，则返回 null。

实现有ConcurrentSkipListSet, TreeSet