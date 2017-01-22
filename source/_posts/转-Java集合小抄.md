---
title: '[转]Java集合小抄'
date: 2017-01-18 15:18:39
categories: "Java"
tags:
- 学习
---
# 集合 #
## List ##
### ArrayList ###
- 以数组实现，节约空间。但是数组容量限制，超出限制会增加50%容量，用System.arraycopy()复制到新的数组。因此最好能给出数组大小的预估值。
- 默认第一次大小为10。
<!-- more -->
- 按下标访问元素，get(下标获取元素)、set(替换下标元素)的性能很高，
是数组的基本优势。
- 按下标插入元素，删除元素，add(i,e)、remove(i)、remove(e),则会用到System.arraycopy()来复制移动受影响的元素,性能会变差。
- 越是前面的元素，修改的时候移动的元素越多。用add(e)在尾部添加元素、删除最后一个元素不会影响性能。
### LinkedList ###
- 以双向链表实现，链表无容量限制，但是双向链表本身使用了更多空间，每插入一个元素都要构造一个额外的Node对象，也需要额外的指针操作。
- 按数组下标访问元素，get(i)、set(i,e),需要移动到指定Node节点(i>节点个数时从尾部移动到头部)
- 插入、删除元素时修改前后节点指针即可
- 只有在两头add()、addFirst()、addLast()、removeFirst()、removeLast()才能省掉指针的移动。

### Iterator ###
Iterator 支持从集合中安全删除对象，只需在Iterator上调用remove().
ArrayList继承了AbstractList，而AbstractList有定义
```java
        /**
         * The modCount value that the iterator believes that the backing
         * List should have.  If this expectation is violated, the iterator
         * has detected concurrent modification.
         */
        int expectedModCount = modCount;
        ...
        final void checkForComodification() {
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
        }
        ...
```
`checkForComodification`这个方法是检查modCount和expectedModCount的值是否是相对，如果不相等则抛出`ConcurrentModificationException`异常。
这是因为在多线程中操作容器时，其他线程可能已经改变了容器的内容，所以每次对容器进行操作的时候modCount都会+1。当Iterator遍历检查到modCount变化是会马上抛出异常，这是Java的`fail-fast`机制。
而Iterator的remove方法在操作完后让expectedModCount和modCount在此相等
## Map ##
### HashMap ###
- 以Enty[]数组实现的哈希桶数组，用Key的哈希值取模桶数组的大小可以的到数组的下标
- 插入元素时，如果两条Key落在同一个桶，称之为哈希冲突或者碰撞
- 哈希冲突JDK8之前是用的是链表法，用Entry用一个next属性实现多个Entry以单向链表的形式存放。然后遍历链表中的所有元素，逐一比较Key值
- 在JDK8后，新增链表的阈值为8，链表的元素数量超过阈值时改用红黑树来存储，提高查找速度。
- 当Entry数量达到数组的75%，数组成倍扩容，重新分配原来的Entry，扩容成本不低。
### LinkedHashMap ###
- 扩展HashMap，每个Entry增加双向链表，非常占内存的数据结构
### ConcurrentSkipListMap ###
- JDK6新增并发优化的SortedMap，以SkipList结构实现，支持CAS无锁算法。

** --待整理-- **
# 线程 #
方法区和堆一样，是线程共享的。在方法区中，存储每个类的信息（类名，方法信息，字段信息）、静态变量、常量以及编译器编译后的代码。

# 基本数据类型 #
## int -> Integer ##
> Integer a = 59;
> int b = 59;
> Integer c = Integer.valueOf(59);
> Integer d = new Integer(59);

a 会调用`valueOf`方法 这个方法返回的是一个Integer对象。下面是它的源码
```java
public static Integer valueOf(int i) {
    assert IntegerCache.high >= 127;
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```
可以看出当i的值在[-128,127]而且在`IntegerCache`中存在此对象，就直接返回引用，没有的话创建一个新的对象。
显然在这个a之前内存还没有59这个值，所有它创建了一个Integer对象
b 是基本类型，存储在栈中
c 也用了`valueOf`这个方法,此时IntegerCache已经存在这个对象，返回引用。
d 是一个新的Integer对象
在比较int和Integer值时，Integer会调用`intValue`自动拆箱成int，进行值比较。
