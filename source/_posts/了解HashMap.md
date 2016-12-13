---
title: HashMap,Hashtable,ConcurrentHashMap,SynchronizedMap的原理与区别
date: 2016-12-07 10:28:18
categories: "Java"
tags:
- 学习
---
## HashMap ##
### HashMap的碰撞处理 ###
HashMap通过hashCode()方法来确定元素存储的bucketIndex位置，不同的Key有概率hash是相同的。
两个不同Key的hash值相同时，HashMap通过单链表方式，将新元素加入链表表头，通过next指向原有元素。
<!-- more -->
** 在JDK1.8版本中，只要bucket中的链表长度超过阈值（8）时，会将链表转化为红黑树**
在JDK1.7中HashMap的put方法源码如下：
```java
 public V put(K key, V value) {
        ...
        //处理Key为null
        if (key == null)
            return putForNullKey(value);
        //得到key的hash码
        int hash = hash(key);
        //由hash码获取bucketIndex下标
        int i = indexFor(hash, table.length);
        //取出bucketIndex上元素，形成单链表
        for (Entry<K,V> e = table[i]; e != null; e = e.next) {
            Object k;
            //hash码相同时且对象相同时
            if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
                //替换旧值
                V oldValue = e.value;
                e.value = value;
                e.recordAccess(this);
                return oldValue;
            }
        }
        //key不存在，加入新元素
        modCount++;
        addEntry(hash, key, value, i);
        return null;
    }
```

### 为什么HashMap线程不安全 ###
1. 并发时，多线程同时操作使用put方法添加元素
，如果发生碰撞，可能会导致两个值添加到同一位置，致使最终有一个值被覆盖
2. 多线程使用HashMap进行扩容时，可能会形成循环链路，详情可以看看[Java HashMap的死循环](http://coolshell.cn/articles/9606.html)

