---
layout: post
title: java collection
---

# HashSet/HashMap
HashSet可以认为是对HashMap的一个封装，把Set中的对象作为HashMap的Key（Map的Key不允许重复，具有跟Set一样的特性）（所有的Key都对应一个Dummy Object）。

## 测试例

### HashMap
JDK 6，7中，HashMap有三个测试例：
* KeySetRemove
* SetValue
* ToString

JDK8有增加了4个测试例：
* HashMapCloneLeak
* NullKeyAtResize
* OverrideIsEmpty
* ReplaceExisting

JDK9又增加了一个
* PutNullKey

### HashSet
HashSet仅在JDK8中增加了一个测试例。在JDK 6, 7中都无。
* Serialization

## 实现
## HashMap

参考[这篇文章](https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)

binned HashTable (有一个 `Node<K, V>[] table` field)。
与HashTable类似，但是**unsynchronized and permits nulls**。需要线程安全时，Java 5以上推荐使用ConcurrentHashMap。HashTable基本上过时了。另外`Collections.synchronizeMap()`可以把HashMap改造为同步的。但HashTable和synchronizedMap都是对整个集合加锁，性能不好。ConcurrentHashMap引入了分割，仅仅需要锁定map的某个部分。

capacity是bucket的数目。
loadFactor: 当entry/bucket超过loadFactor时，扩容。

每个buckets中的元素，如有多个，则以链表的形式存放。当链表长度超过TREEIFY_THRESHOLD（从JDK8开始，默认为8），则转换为红黑树（查找时间O(logn)）。

Iterator按bucket遍历，因此是乱序。



