
- [HashMap](#hashmap)
  - [1. HashMap是什么？它是如何工作的？](#1-hashmap是什么它是如何工作的)
  - [2. HashMap的容量是如何确定的？](#2-hashmap的容量是如何确定的)
  - [3. HashMap的实现原理是什么？](#3-hashmap的实现原理是什么)
  - [4. HashMap和Hashtable有什么区别？](#4-hashmap和hashtable有什么区别)
  - [5. 如何避免HashMap中的冲突？](#5-如何避免hashmap中的冲突)
  - [6. 为什么HashMap线程不安全?](#6-为什么hashmap线程不安全)
  - [7. HashMap里，什么是散列分布均匀，为什么要散列分布均匀?](#7-hashmap里什么是散列分布均匀为什么要散列分布均匀)

[toc]

## HashMap

### 1. HashMap是什么？它是如何工作的？

HashMap是Java中的一个集合类，用于存储键值对。它基于哈希表实现，使用哈希算法来计算键的哈希码，然后将键值对存储在哈希表的对应位置。当需要查找键值对时，HashMap会使用相同的哈希算法计算键的哈希码，并在哈希表中查找对应位置的键值对。

### 2. HashMap的容量是如何确定的？

HashMap的容量是在创建HashMap对象时指定的。它会根据指定的初始容量和负载因子来确定哈希表的大小。负载因子是一个浮点数，表示哈希表的填充比例。当哈希表中的键值对数量超过负载因子乘以容量时，哈希表会自动进行扩容，以保证哈希表的性能。

### 3. HashMap的实现原理是什么？

HashMap的实现原理基于哈希表，它使用哈希算法来计算键的哈希码，并将键值对存储在哈希表的对应位置。当需要查找键值对时，HashMap会使用相同的哈希算法计算键的哈希码，并在哈希表中查找对应位置的键值对。如果有多个键值对存储在同一个位置，HashMap会使用链表或红黑树等数据结构来存储这些键值对，以提高查找效率。

### 4. HashMap和Hashtable有什么区别？

HashMap和Hashtable都是用于存储键值对的集合类，但它们有以下区别：

- HashMap是非线程安全的，而Hashtable是线程安全的。
- HashMap允许键和值为null，而Hashtable不允许。
- HashMap的迭代器是fail-fast的，而Hashtable的迭代器不是。
- HashMap是JDK 1.2引入的，而Hashtable是JDK 1.0引入的，已经被废弃了。

### 5. 如何避免HashMap中的冲突？

为了避免HashMap中的冲突，可以使用以下方法：

- 选择合适的初始容量和负载因子。
- 实现hashCode()方法和equals()方法，以确保键的唯一性。
- 尽量避免使用可变对象作为键。
- 在并发环境下，可以考虑使用ConcurrentHashMap等线程安全的集合类。

### 6. 为什么HashMap线程不安全?

HashMap是线程不安全的主要原因是它的内部结构是基于哈希表实现的，并且没有进行同步措施来保证多线程环境下的安全性。具体原因如下：

1. 并发修改导致的数据不一致：当多个线程同时对HashMap进行修改操作时，可能会导致数据不一致的情况。例如，一个线程正在进行扩容操作，而另一个线程同时进行插入操作，可能会导致某些键值对丢失或者重复插入。

2. 链表环形引用导致的死循环：在JDK 1.7及之前的版本中，当哈希表中的链表长度达到一定阈值时，会将链表转换为红黑树来提高查找效率。但是，在多线程环境下，如果两个线程同时对同一个链表进行插入操作，可能会导致链表中的节点形成环形引用，从而导致死循环。

3. 不正确的迭代器使用：HashMap的迭代器是fail-fast的，即在迭代过程中如果有其他线程对HashMap进行修改操作，会抛出ConcurrentModificationException异常。这是因为迭代器在创建时会记录一个modCount值，表示HashMap的修改次数。当迭代器进行next操作时，会检查modCount值是否发生变化，如果发生变化则抛出异常。但是，如果在迭代过程中有其他线程对HashMap进行修改操作，可能会导致modCount值发生变化，从而导致迭代器抛出异常。

为了在多线程环境下安全地使用HashMap，可以考虑使用线程安全的ConcurrentHashMap或者使用同步措施来保证HashMap的安全性，例如使用Collections.synchronizedMap方法包装HashMap，或者使用锁来对HashMap进行同步操作。

### 7. HashMap里，什么是散列分布均匀，为什么要散列分布均匀?
散列分布均匀是指在哈希表中，键的哈希码被均匀地分布在不同的位置上。也就是说，尽量避免多个键的哈希码映射到同一个位置上，以减少哈希冲突的概率。

散列分布均匀的好处是可以提高哈希表的性能。当键的哈希码均匀地分布在不同的位置上时，查找键值对的时间复杂度可以接近O(1)，因为只需要计算键的哈希码并在哈希表中查找对应位置的键值对。而如果多个键的哈希码映射到同一个位置上，就需要遍历链表或红黑树等数据结构来查找键值对，时间复杂度可能会变为O(n)。

为了实现散列分布均匀，可以采取以下措施：

1. 选择合适的初始容量和负载因子：初始容量和负载因子可以影响哈希表的填充比例。当哈希表的填充比例适中时，可以减少哈希冲突的概率。

2. 实现hashCode()方法：hashCode()方法用于计算键的哈希码。应该尽量保证hashCode()方法返回的哈希码分布均匀，避免多个键的哈希码映射到同一个位置上。

3. 使用好的哈希函数：哈希函数可以将键的哈希码映射到哈希表的位置。选择好的哈希函数可以减少哈希冲突的概率，提高散列分布的均匀性。

通过以上措施，可以尽量保证哈希表中键的哈希码分布均匀，减少哈希冲突的概率，从而提高哈希表的性能。

### 8. 聊一聊java的集合类
当面试官问到Java的集合类时，我会很高兴地与他聊一聊。Java的集合类是Java编程中非常重要和常用的一部分，它提供了一系列的数据结构和算法，方便我们进行数据的存储、操作和管理。

首先，Java的集合类可以分为两大类：一类是基于接口的集合类，如List、Set和Map；另一类是基于抽象类的集合类，如AbstractList、AbstractSet和AbstractMap。这些集合类都实现了Java集合框架中定义的接口和抽象类，提供了统一的操作和使用方式。

其中，List是有序的集合，可以存储重复的元素，常用的实现类有ArrayList和LinkedList。ArrayList是基于数组实现的，适合随机访问和修改操作；LinkedList是基于链表实现的，适合插入和删除操作。

Set是无序的集合，不允许存储重复的元素，常用的实现类有HashSet和TreeSet。HashSet是基于哈希表实现的，查找和插入操作的时间复杂度为O(1)；TreeSet是基于红黑树实现的，元素会按照自然排序或者自定义的比较器进行排序。

Map是键值对的集合，每个键对应一个值，常用的实现类有HashMap和TreeMap。HashMap是基于哈希表实现的，查找和插入操作的时间复杂度为O(1)；TreeMap是基于红黑树实现的，键会按照自然排序或者自定义的比较器进行排序。

此外，Java的集合类还提供了一些辅助类和接口，如Collections类用于操作集合，Comparator接口用于比较元素的大小。

在使用Java的集合类时，需要根据实际需求选择合适的集合类，并根据集合类的特点和性能进行使用和操作。同时，需要注意多线程环境下的安全性，可以选择线程安全的集合类或者使用同步措施来保证集合的安全性。

总的来说，Java的集合类是非常强大和灵活的，可以满足各种数据处理和管理的需求，是Java编程中不可或缺的一部分。

### 9. 什么是红黑树，可以用你的理解说一下吗？
红黑树是一种自平衡的二叉搜索树，它在插入和删除节点时会自动进行调整，以保持树的平衡。红黑树的名字来源于节点上的颜色，每个节点可以是红色或黑色。

红黑树具有以下特性：

1. 每个节点要么是红色，要么是黑色。
2. 根节点是黑色的。
3. 所有叶子节点（空节点）都是黑色的。
4. 如果一个节点是红色的，那么它的两个子节点都是黑色的。
5. 对于任意节点，从该节点到其所有后代叶子节点的简单路径上，均包含相同数量的黑色节点。

这些特性保证了红黑树的平衡性和搜索效率。通过保持特性4和特性5，红黑树的最长路径不会超过最短路径的两倍，使得整棵树的高度保持在O(log n)的范围内。

在插入和删除节点时，红黑树会根据特性进行调整，以保持平衡。插入节点时，根据节点的值和特性，将节点插入到合适的位置，并进行颜色和结构的调整。删除节点时，也会根据节点的值和特性，删除节点，并进行颜色和结构的调整。

红黑树的平衡性和高效性使得它在很多场景下被广泛应用，比如在Java的集合类中的TreeMap就是基于红黑树实现的。红黑树的设计和算法虽然复杂，但是它提供了高效的插入、删除和搜索操作，是一种非常重要和有用的数据结构。

### 10. 比较分析一下HashMap和ConcurrentHashMap

1. 数据结构和实现原理：
  - HashMap的底层数据结构是数组和链表/红黑树。它使用哈希函数将元素映射到数组的索引位置，并使用链表/红黑树解决哈希冲突。当链表长度过长时，链表会转换为红黑树，以提高查找效率。
  - ConcurrentHashMap在HashMap的基础上加入了并发控制。它使用了分段锁的方式实现并发访问，将整个数据结构分成多个段，每个段都有自己的锁。这样多个线程可以同时访问不同的段，从而提高并发性能。

2. 特性和用法：
  - HashMap和ConcurrentHashMap都是键值对的集合类，可以存储任意类型的键和值。
  - HashMap允许使用null作为键和值，而ConcurrentHashMap不允许。
  - HashMap的插入、删除和查找操作的时间复杂度为O(1)，但在哈希冲突较多时，可能会退化为O(n)。ConcurrentHashMap的性能与并发控制相关，但通常情况下也能达到O(1)的时间复杂度。
  - HashMap和ConcurrentHashMap都可以通过迭代器遍历集合中的元素。

3. 优缺点：
  - HashMap的优点是插入、删除和查找操作的时间复杂度较低，适用于单线程环境。但在并发环境下，HashMap不是线程安全的，需要额外的同步措施。
  - ConcurrentHashMap的优点是在并发环境下提供了线程安全的操作，通过分段锁实现了较好的并发性能。它适用于高并发的场景。但相比于HashMap，ConcurrentHashMap的实现更加复杂，消耗更多的内存。

4. 注意事项：
  - 在使用HashMap和ConcurrentHashMap时，需要注意线程安全性。如果在多线程环境下使用HashMap，需要进行额外的同步措施，比如使用Collections.synchronizedMap()方法包装。
  - HashMap的初始容量和负载因子会影响性能，需要根据实际情况进行调整。
  - 在遍历HashMap和ConcurrentHashMap时，需要注意并发修改的问题。可以使用迭代器或者使用并发安全的遍历方式，如ConcurrentHashMap的forEach()方法。

通过理论学习、实践编码和性能分析，结合实际项目经验，可以逐步提升对HashMap和ConcurrentHashMap的掌握程度。同时，可以通过阅读相关的书籍和文档，参与开源项目或者实践项目来进一步深入学习和应用。

### 11. ConcurrentHashMap是如何插入、删除、查找数据、扩容的？在什么情况下如何保证了线程安全？请给出例子、源码详细说明

ConcurrentHashMap在插入、删除、查找数据和扩容时，通过使用分段锁（Segment）来实现线程安全。每个Segment都是一个独立的哈希表，包含一个数组和一个链表/红黑树。下面是对每个操作的详细说明：

1. 插入数据：
  - 首先，根据键的哈希值计算出在哪个Segment中进行操作。
  - 然后，获取该Segment的锁，保证只有一个线程可以操作该Segment。
  - 接着，在该Segment中进行插入操作，如果发生哈希冲突，则使用链表/红黑树解决冲突。
  - 最后，释放锁。

2. 删除数据：
  - 同样地，根据键的哈希值计算出在哪个Segment中进行操作。
  - 获取该Segment的锁。
  - 在该Segment中查找要删除的键，并进行删除操作。
  - 释放锁。

3. 查找数据：
  - 根据键的哈希值计算出在哪个Segment中进行操作。
  - 获取该Segment的锁。
  - 在该Segment中查找要查找的键，并返回对应的值。
  - 释放锁。

4. 扩容：
  - 当HashMap的元素个数达到阈值时，会触发扩容操作。
  - 扩容时，会创建一个新的数组和链表/红黑树，将原来的元素重新分配到新的数组中。
  - 在扩容过程中，会对每个Segment进行分段锁的更新，以保证并发访问的正确性。

线程安全保证：
ConcurrentHashMap通过分段锁的方式实现线程安全。每个Segment都有自己的锁，不同线程可以同时访问不同的Segment，从而提高并发性能。只有当多个线程同时访问同一个Segment时，才需要获取该Segment的锁，保证同一时刻只有一个线程可以操作该Segment。这样，就可以在并发环境下保证线程安全性。

下面是ConcurrentHashMap的部分源码，以便更详细地说明其实现原理：

```java
public class ConcurrentHashMap<K, V> {
    // 定义Segment数组
    private final Segment[] segments;
    
    // 定义Segment内部类
    static final class Segment<K, V> {
        // 定义Segment内部的哈希表
        transient volatile Node<K, V>[] table;
        // 定义Segment的锁
        transient final ReentrantLock lock = new ReentrantLock();
        
        // 插入数据
        void put(K key, V value) {
            lock.lock();
            try {
                // 在Segment中进行插入操作
                // 处理哈希冲突等
            } finally {
                lock.unlock();
            }
        }
        
        // 删除数据
        void remove(K key) {
            lock.lock();
            try {
                // 在Segment中进行删除操作
            } finally {
                lock.unlock();
            }
        }
        
        // 查找数据
        V get(K key) {
            lock.lock();
            try {
                // 在Segment中进行查找操作
                return null;
            } finally {
                lock.unlock();
            }
        }
        
        // 扩容
        void resize() {
            Node<K, V>[] oldTable = table;
            // 创建新的数组和链表/红黑树
            // 将原来的元素重新分配到新的数组中
            // 更新Segment的锁
        }
    }
    
    // 插入数据
    public void put(K key, V value) {
        int hash = hash(key);
        // 根据哈希值计算出在哪个Segment中进行操作
        Segment<K, V> segment = segmentForHash(hash);
        segment.put(key, value);
    }
    
    // 删除数据
    public void remove(K key) {
        int hash = hash(key);
        Segment<K, V> segment = segmentForHash(hash);
        segment.remove(key);
    }
    
    // 查找数据
    public V get(K key) {
        int hash = hash(key);
        Segment<K, V> segment = segmentForHash(hash);
        return segment.get(key);
    }
    
    // 扩容
    private void resize() {
        for (Segment<K, V> segment : segments) {
            segment.resize();
        }
    }
    
    // 根据哈希值计算出在哪个Segment中进行操作
    private Segment<K, V> segmentForHash(int hash) {
        return segments[(hash >>> segmentShift) & segmentMask];
    }
    
    // 计算哈希值
    private int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
}
```

以上是ConcurrentHashMap的部分源码，展示了其插入、删除、查找数据和扩容的实现。通过分段锁和Segment的方式，ConcurrentHashMap实现了线程安全。不同线程可以同时访问不同的Segment，从而提高并发性能。只有在多个线程同时访问同一个Segment时，才需要获取该Segment的锁，保证同一时刻只有一个线程可以操作该Segment。这样，就可以在并发环境下保证线程安全性。



### 12. 请说一下，jdk1.8版本Hashmap的查询、增加、删除、扩容是如何实现的？

在JDK 1.8版本中，HashMap的查询、增加、删除、扩容是如下实现的：

1. 查询（get）操作：
  - 根据key的hashCode计算出对应的hash值。
  - 根据hash值计算出在数组中的索引位置。
  - 遍历该索引位置上的链表或红黑树，找到对应的节点。

2. 增加（put）操作：
  - 根据key的hashCode计算出对应的hash值。
  - 根据hash值计算出在数组中的索引位置。
  - 如果该索引位置上没有节点，则直接将新节点插入。
  - 如果该索引位置上已经存在节点，则遍历链表或红黑树，如果找到相同的key，则更新value；如果没有找到相同的key，则将新节点插入到链表或红黑树的末尾。

3. 删除（remove）操作：
  - 根据key的hashCode计算出对应的hash值。
  - 根据hash值计算出在数组中的索引位置。
  - 遍历该索引位置上的链表或红黑树，找到对应的节点并删除。

4. 扩容（resize）操作：
  - 当HashMap中的元素个数超过负载因子（默认为0.75）与当前容量的乘积时，就会进行扩容。
  - 扩容时，将容量翻倍，并重新计算每个节点在新数组中的索引位置。
  - 将原来的链表或红黑树节点重新分配到新数组中。

### 13. 为什么HashMap的容量要求是2的次幂呢？

这是为了优化计算索引位置的性能。在计算索引位置时，HashMap会使用hash值与数组的长度进行位运算，这样可以保证计算出的索引位置更分散，减少了碰撞的概率，提高了查询、增加和删除操作的效率。如果容量是2的次幂，那么位运算就可以直接使用位与操作，而不需要进行取模运算，这样可以进一步提高性能。另外，容量为2的次幂也方便进行扩容操作，只需要进行位移操作即可。

当HashMap的容量为2的次幂时，可以直接使用位与操作来计算节点在数组中的索引位置，而不需要进行取模运算。

假设HashMap的容量为16，即数组的长度为16。当计算节点的索引位置时，通常会使用节点的hash值与数组长度减一进行取模运算，即 `index = hash % length`。但是，当数组的长度为2的次幂时，可以将取模运算转化为位与操作，即 `index = hash & (length - 1)`。

例如，假设节点的hash值为22，数组的长度为16。使用取模运算计算索引位置时，`index = 22 % 16 = 6`。而使用位与操作计算索引位置时，`index = 22 & (16 - 1) = 22 & 15 = 6`。可以看到，结果是相同的。

通过位与操作来计算索引位置可以提高性能，因为位运算比取模运算更高效。位与操作只需要进行位运算，而取模运算需要进行除法运算，除法运算的性能较低。

另外，当HashMap需要进行扩容时，容量为2的次幂也方便进行位移操作。扩容时，只需要将容量翻倍，并将原来的节点重新分配到新数组中。例如，将容量从16扩容到32时，只需要进行一次位移操作，即将原来的索引位置左移一位即可。

综上所述，容量为2的次幂可以通过位运算来计算索引位置，提高性能，并且方便进行扩容操作。

### 14. Hashmap的对象为什么重写equal方法，hashcode方法？
HashMap是一种基于哈希表实现的Map接口，它的底层数据结构是数组和链表或红黑树。在使用HashMap时，需要重写对象的equals方法和hashCode方法，以便HashMap能够正确地进行键值对的查找、插入和删除操作。

为什么要重写equals方法呢？因为在HashMap中，键值对的查找是根据键对象的equals方法来判断的。如果两个键对象的equals方法返回true，那么HashMap就认为它们是相同的键，会用后面的值覆盖前面的值。因此，如果不重写equals方法，那么HashMap在查找键值对时就无法正确判断两个键是否相等，会导致出现重复的键或丢失键值对的情况。

为什么要重写hashCode方法呢？因为在HashMap中，键值对的存储是根据键对象的hashCode方法来确定的。HashMap会根据键对象的hashCode值计算出在数组中的索引位置，并将键值对存储在该位置上。如果两个键对象的hashCode方法返回的值不同，那么它们在数组中的索引位置也会不同，即使它们的equals方法返回true。因此，如果不重写hashCode方法，那么HashMap在存储键值对时就无法正确计算出索引位置，会导致出现重复的键或丢失键值对的情况。

因此，为了保证HashMap能够正确地进行键值对的查找、插入和删除操作，需要重写对象的equals方法和hashCode方法，使它们能够正确地判断两个对象是否相等，并且能够正确地计算出在数组中的索引位置。

### 15. 为什么不直接用父类Object对象的hashCode方法？有什么问题吗？

父类Object对象的hashCode方法是根据对象的内存地址计算出的一个整数值。在Java中，每个对象都有一个唯一的内存地址，因此默认情况下，不同的对象的hashCode值是不相同的。

然而，在实际应用中，我们常常需要根据对象的属性来判断对象是否相等，而不仅仅是根据内存地址。例如，在使用HashMap时，我们希望根据键对象的属性来判断两个键对象是否相等，而不仅仅是根据内存地址。如果直接使用父类Object对象的hashCode方法，那么不同的对象即使属性相同，它们的hashCode值也会不相同，这就会导致HashMap无法正确地判断两个键对象是否相等。

因此，为了能够根据对象的属性来判断对象是否相等，我们需要重写对象的equals方法和hashCode方法。重写equals方法可以根据对象的属性来判断两个对象是否相等，而重写hashCode方法可以根据对象的属性来计算出一个整数值，使得相等的对象具有相同的hashCode值。

重写equals方法和hashCode方法的目的是为了保证HashMap能够正确地进行键值对的查找、插入和删除操作。如果不重写equals方法和hashCode方法，那么HashMap在查找键值对时就无法正确判断两个键是否相等，会导致出现重复的键或丢失键值对的情况。因此，重写equals方法和hashCode方法是为了保证HashMap的正确性和稳定性。


### 16. 详细讲解一下Hashmap的遍历方式
HashMap的遍历方式有多种，下面我会详细介绍四种常用的遍历方式：

1. 使用EntrySet遍历（推荐）：
   ```java
   Map<K, V> map = new HashMap<>();
   // 添加键值对
   // ...
   
   for (Map.Entry<K, V> entry : map.entrySet()) {
       K key = entry.getKey();
       V value = entry.getValue();
       // 处理键值对
       // ...
   }
   ```
   这种方式通过调用`entrySet()`方法获取Map中的所有键值对，然后使用增强for循环遍历每个键值对，通过`getKey()`方法获取键，通过`getValue()`方法获取值。

2. 使用KeySet遍历：
   ```java
   Map<K, V> map = new HashMap<>();
   // 添加键值对
   // ...
   
   for (K key : map.keySet()) {
       V value = map.get(key);
       // 处理键值对
       // ...
   }
   ```
   这种方式通过调用`keySet()`方法获取Map中的所有键，然后使用增强for循环遍历每个键，通过`get(key)`方法获取对应的值。

3. 使用Values遍历：
   ```java
   Map<K, V> map = new HashMap<>();
   // 添加键值对
   // ...
   
   for (V value : map.values()) {
       // 处理值
       // ...
   }
   ```
   这种方式通过调用`values()`方法获取Map中的所有值，然后使用增强for循环遍历每个值。

4. 使用Iterator遍历：
   ```java
   Map<K, V> map = new HashMap<>();
   // 添加键值对
   // ...
   
   Iterator<Map.Entry<K, V>> iterator = map.entrySet().iterator();
   while (iterator.hasNext()) {
       Map.Entry<K, V> entry = iterator.next();
       K key = entry.getKey();
       V value = entry.getValue();
       // 处理键值对
       // ...
   }
   ```
   这种方式通过调用`entrySet().iterator()`方法获取Map中所有键值对的迭代器，然后使用`hasNext()`方法判断是否还有下一个键值对，使用`next()`方法获取下一个键值对，通过`getKey()`方法获取键，通过`getValue()`方法获取值。

以上四种遍历方式中，推荐使用第一种方式（EntrySet遍历），因为它在遍历过程中可以同时获取键和值，效率较高。另外，需要注意的是，在遍历过程中不要修改Map的结构（如添加或删除键值对），否则可能会引发ConcurrentModificationException异常。


### 17. 为什么不允许在遍历时添加或删除键值对？为什么会报这个错？如果想要遍历添加或删除键值对，该怎么做？

在遍历过程中添加或删除键值对会导致HashMap的结构发生变化，这可能会导致遍历操作无法正常进行。为了保证HashMap的一致性和稳定性，Java设计了一种机制来防止在遍历过程中对HashMap的结构进行修改，即通过使用modCount和expectedModCount这两个计数器来检测并防止并发修改。

在HashMap的实现中，modCount是用来记录HashMap结构修改的次数的计数器，而expectedModCount是用来记录在遍历过程中期望的HashMap结构修改次数的计数器。在遍历过程中，如果modCount和expectedModCount不相等，就会抛出ConcurrentModificationException异常，表示HashMap的结构已经发生了修改。

这样设计的目的是为了避免在遍历过程中出现不一致的情况，保证遍历操作的正确性。如果允许在遍历时添加或删除键值对，就会导致遍历过程中的expectedModCount与实际的modCount不相等，从而引发ConcurrentModificationException异常。

如果确实需要在遍历过程中添加或删除键值对，可以使用迭代器的remove方法来删除键值对，或者使用Map的put方法来添加键值对。这样可以保证在遍历过程中对HashMap的结构进行修改，同时也会更新modCount和expectedModCount计数器，避免抛出ConcurrentModificationException异常。

### 18. 为什么在遍历过程中添加或删除键值对会导致HashMap的结构发生变化，会导致遍历操作无法正常进行？可以举例说明吗
在遍历过程中添加或删除键值对会导致HashMap的结构发生变化的原因是，HashMap内部是通过哈希表来存储键值对的，添加或删除键值对会改变哈希表中的元素位置，从而导致遍历操作无法正常进行。

举个例子来说明，假设有一个HashMap包含以下键值对：

```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);
map.put("C", 3);
```

当我们使用迭代器遍历这个HashMap时，HashMap内部会按照一定的规则将键值对存储在哈希表的不同位置上。假设在遍历过程中，我们想要删除键为"B"的键值对：

```java
Iterator<Map.Entry<String, Integer>> iterator = map.entrySet().iterator();
while (iterator.hasNext()) {
    Map.Entry<String, Integer> entry = iterator.next();
    String key = entry.getKey();
    if (key.equals("B")) {
        iterator.remove(); // 删除键为"B"的键值对
    }
}
```

在删除键为"B"的键值对后，HashMap的结构发生了变化，此时原本在哈希表中的位置可能已经被其他键值对占据，导致迭代器无法继续正常遍历。如果继续遍历，可能会出现遍历到重复或丢失某些键值对的情况。

为了避免这种情况，Java设计了ConcurrentModificationException异常来提醒开发者在遍历过程中不要修改HashMap的结构。如果确实需要在遍历过程中添加或删除键值对，可以使用迭代器的remove方法来删除键值对，或者使用Map的put方法来添加键值对。这样可以保证在遍历过程中对HashMap的结构进行修改，同时也会更新modCount和expectedModCount计数器，避免抛出ConcurrentModificationException异常。

### 19. 迭代器遍历的原理是什么

迭代器是一种用于遍历集合类的对象，它提供了一种统一的方式来访问集合中的元素，而不需要了解集合内部的具体实现细节。

在Java中，迭代器模式的核心是Iterator接口。该接口定义了一些方法来遍历集合，包括：hasNext()、next()和remove()。

- hasNext()方法用于判断集合中是否还有下一个元素，如果有则返回true，否则返回false。
- next()方法用于获取集合中的下一个元素，并将迭代器的指针移动到下一个位置。
- remove()方法用于从集合中移除通过next()方法获取的元素。

迭代器的遍历过程是通过不断调用hasNext()和next()方法来实现的。在遍历过程中，迭代器会维护一个指针指向当前位置，每次调用next()方法都会返回当前位置的元素，并将指针移动到下一个位置。

具体来说，迭代器的遍历过程如下：

1. 创建一个迭代器对象，通常是通过调用集合的iterator()方法来获取。
2. 使用while循环和hasNext()方法来判断是否还有下一个元素。
3. 在循环内部，使用next()方法获取当前位置的元素，并处理该元素。
4. 可选地，在循环内部使用remove()方法来移除元素。

迭代器遍历的好处是可以在遍历过程中进行添加、删除等操作，而不会导致ConcurrentModificationException异常。这是因为迭代器在遍历过程中会维护一个expectedModCount计数器，用于检测并防止并发修改。如果在遍历过程中对集合进行了修改，expectedModCount计数器会与实际的modCount计数器不一致，从而抛出ConcurrentModificationException异常。



### 20. 多个线程同时扩容时为什么会出现环形链表？

//扩容后将数据填充进新桶
```java
    void transfer(Entry[] newTable, boolean rehash) {
        int newCapacity = newTable.length;//新的容量  
        for (Entry e : table) {
            while(null != e) {
                Entry next = e.next;
                if (rehash) {
                    e.hash = null == e.key ? 0 : hash(e.key);
                }
                int i = indexFor(e.hash, newCapacity);//定位Hash桶，计算的结果可能为：初始位置 或者 初始位置 + 扩容量
                e.next = newTable[i];//扩容插入也会采用头插法，与旧的hash桶相比链表的顺序可能会被颠倒，并且分散到 初始位置 和 初始位置 + 扩容量两个位置中
                newTable[i] = e;
                e = next;
            }
        }
    }
```
假如HashMap同一个链表里有 a、b两个元素，a->b，两个线程同时插入，开始进行扩容。
扩容会将原节点重新分配到新数组，扩容代码有一行 next = e.next，其中e是当前遍历的元素，next是e的下一个元素，
第一个线程执行到了这一行，停止执行，获取到e为a，next为b，第二个线程获得cpu资源开始执行，因为使用的头插法，当第二个线程扩容完毕，此时为b->a，线程1获得cpu资源，开始执行，后面会执行e.next =  newTable[i] ，a又重新指向了b，第一个线程导致了b指向a，出现了循环，导致了死锁问题。

## List Set

### 21. Java编程语言里，为什么Set是无序的集合，List是有序的集合？

在 Java 编程语言中，Set 是无序的集合，而 List 是有序的集合。这是因为它们在内部实现上使用了不同的数据结构。

Set 是基于哈希表实现的，例如 HashSet 和 LinkedHashSet。哈希表是一种使用哈希函数将元素映射到桶中的数据结构。哈希表中的元素是无序的，因为元素的存储位置是根据哈希函数计算得出的。因此，Set 中的元素没有特定的顺序。

List 则是基于数组或链表实现的，例如 ArrayList 和 LinkedList。数组是一种有序的数据结构，它在内存中按照连续的位置存储元素。因此，List 中的元素按照它们在数组或链表中的顺序进行存储和访问，具有特定的顺序。

需要注意的是，虽然 List 是有序的集合，但并不意味着它是按照元素的大小或者插入顺序进行排序的。List 中的元素可以根据需要进行插入、删除和修改，而不会改变它们的相对顺序。如果需要对 List 进行排序，可以使用 Collections 类的 sort 方法或者使用其他排序算法来实现。


### 22. 可以再详细解释一下有序和无序的区别吗？

有序和无序是集合中的两个重要概念，它们的区别如下：

1. 有序集合中的元素是按照一定的顺序排列的，而无序集合中的元素没有特定的顺序。

2. 对于有序集合，元素的顺序是固定的，不会随着插入和删除操作的执行而改变。而对于无序集合，元素的顺序是不确定的，可能会随着插入和删除操作的执行而发生变化。

3. 在有序集合中，可以根据元素的位置进行操作，例如获取某个位置上的元素、获取指定范围内的元素等。而在无序集合中，只能根据元素的值进行操作，例如判断元素是否存在、获取元素的个数等。

在Java编程语言中，List是有序集合，元素的顺序是固定的，可以根据元素的位置进行操作。例如，可以使用get()方法获取指定位置上的元素，使用add()方法在指定位置上插入元素，使用remove()方法删除指定位置上的元素等。

而Set是无序集合，元素的顺序是不确定的，只能根据元素的值进行操作。例如，可以使用contains()方法判断元素是否存在，使用add()方法添加元素，使用remove()方法删除元素等。

需要注意的是，虽然Set是无序的集合，但是可以使用LinkedHashSet来创建有序的Set集合。LinkedHashSet是HashSet的子类，它使用链表来维护元素的顺序，因此可以保证元素的插入顺序和访问顺序一致。

### 23. fail-fast机制是针对集合所有List、Set、Map的嘛？具体是什么？

fail-fast机制是Java集合框架中的一种机制，它是针对所有实现了Iterator接口的集合类的。Iterator接口提供了迭代器模式，可以让我们在集合中遍历元素，而fail-fast机制则是为了保证在遍历集合时，如果集合的内容发生了变化，会立即抛出ConcurrentModificationException异常，防止在遍历时出现意外的结果。

具体来说，当我们通过Iterator遍历集合时，如果在遍历过程中集合的内容发生了变化（例如添加、删除元素），就会抛出ConcurrentModificationException异常。这是因为Iterator在遍历时会记录集合的修改次数，如果发现修改次数与遍历时记录的不一致，就会抛出异常。

需要注意的是，fail-fast机制只是一种检测机制，它不能保证所有的并发修改都会被检测到。例如，如果在多线程环境下同时修改了同一个集合，可能会出现一些未被检测到的修改。因此，在多线程环境下使用集合时，需要注意线程安全性，可以选择使用线程安全的集合类，或者使用同步机制来保证线程安全。

### 24. 请从定义、特点、应用场景、不足、不足如何优化这几方面来描述一下HashSet、TreeSet、Hashtable，TreeMap

**HashSet**

定义：HashSet是Java集合框架中的一种Set集合，它是基于HashMap实现的，底层采用HashMap来存储元素，HashSet中的元素是无序的，不允许重复。

特点：
1. HashSet中的元素是无序的。
2. HashSet中的元素不允许重复。
3. HashSet中的元素可以为null。
4. HashSet是非线程安全的。

应用场景：HashSet适用于需要快速查找元素，而不需要保证元素的顺序的场景，比如去重、快速查找等。

不足：HashSet的元素是无序的，如果需要保证元素的顺序，就需要使用其他集合类。

优化：HashSet是基于HashMap实现的，因此可以利用HashMap的一些优化技巧来提高HashSet的性能，比如设置初始容量和负载因子、使用正确的哈希函数等。

**TreeSet**

定义：TreeSet是Java集合框架中的一种Set集合，它是基于TreeMap实现的，底层采用红黑树来存储元素，TreeSet中的元素是有序的，不允许重复。

特点：
1. TreeSet中的元素是有序的。
2. TreeSet中的元素不允许重复。
3. TreeSet是非线程安全的。


应用场景：TreeSet适用于需要保证元素有序且不重复的场景，比如排序、去重等。

不足：TreeSet中的元素不能为null，同时插入、删除、查询的时间复杂度为O(log n)，相对于HashSet较慢。

优化：使用合适的比较器可以提高TreeSet的性能。

**Hashtable**

定义：Hashtable是Java集合框架中的一种Map集合，它是线程安全的，底层采用哈希表来存储键值对，Hashtable中的键和值都不能为null。

特点：
1. Hashtable中的键值对是无序的。
2. Hashtable中的键和值都不能为null。
3. Hashtable是线程安全的。


应用场景：Hashtable适用于需要线程安全的场景，比如多线程环境下的数据共享等。

不足：Hashtable的元素是无序的，同时插入、删除、查询的时间复杂度为O(1)，相对于HashMap较慢。

优化：可以使用ConcurrentHashMap代替Hashtable来提高性能。

Hashtable的底层是数组+链表实现的，当链表长度达到一定阈值时，会将链表转化为红黑树来提高查询效率。

**TreeMap**

TreeMap是Java集合框架中的一种Map集合，它是基于红黑树实现的，底层采用红黑树来存储键值对，TreeMap中的键是有序的，不允许重复。

特点：
1. TreeMap中的键是有序的。
2. TreeMap中的键不允许重复。
3. TreeMap是非线程安全的。


应用场景：TreeMap适用于需要保证键有序且不重复的场景，比如排序、范围查找等。

不足：TreeMap中的键值不能为空，因为红黑树是根据键的比较来构建和维护的，如果键为null，无法进行比较。

优化：可以使用合适的比较器来提高TreeMap的性能。比较器可以自定义实现，也可以使用Java提供的默认比较器，如Comparator.naturalOrder()、Comparator.reverseOrder()等。选择合适的比较器取决于具体的需求，比如按照自然顺序排序还是按照自定义规则排序。

### 25. TreeMap的键可以为null吗？为什么？
一般来说TreeMap的键是不能为空的。因为在执行put方法存值时，会首先判断是否存在比较器，如果创建TreeMap实例时没有传入Comparator比较器，那么程序会对键进行判断，判断它是否为空，如果为空，就会抛出空指针异常。如果我们有特殊需求，是可以自己实现Comparator接口，并重写compare方法去处理掉比较对象为空的情况，这样做也是可以实现在TreeMap中存入一个空值的键的。
注意：TreeSet的底层是用TreeMap实现，即将TreeSet的值作为键存入TreeMap集合中，所以TreeSet存值时跟TreeMap一样的规则

### 26. TreeMap的排序规则（简化版）

TreeSet/TreeMap中key 可以⾃动对 String 类型或8⼤基本类型的包装类型进⾏排序
TreeSet ⽆法直接对⾃定义类型进⾏排序
直接将⾃定义类型添加到 TreeSet/TreeMap中key 会报错 java.lang.ClassCastException
原因： 是因为⾃定义没有实现 java.lang.Comparable 接口（此时，使⽤的是 TreeSet 的⽆参构造器）
对 TreeSet/TreeMap 中 key部分 元素，必须要指定排序规则。主要有两种解决⽅案：
⽅法⼀： 放在集合中的⾃定义类型实现 java.lang.Comparable 接口，并重写 compareTo ⽅法
⽅法⼆： 选择 TreeSet/TreeMap 带⽐较器参数的构造器 ，并从写⽐较器中的 compare ⽅法
此时，在传递⽐较器参数给 TreeSet/TreeMap 构造器时，有 3 种⽅法：
1. 定义⼀个 Comparator 接口的实现类
2. 使⽤匿名内部类
3. lambda 表达式（Comparator 是函数式接口）
   利⽤ -> 的 lambda表达式 重写 compare ⽅法
   利⽤ Comparator.comparing ⽅法
   两种解决⽅案如何选择呢？
1. 当⽐较规则不会发⽣改变的时候，或者说⽐较规则只有⼀个的时候，建议实现 Comparable 接口
2. 当⽐较规则有多个，并且需要在多个⽐较规则之间频繁切换时，建议使⽤ Comparator 接口
需要注意的是，如果键对象既实现了Comparable接口，又传入了Comparator对象，那么Comparator对象的比较规则会覆盖Comparable接口的比较规则。

### 27. TreeMap的排序规则（详细）

TreeMap的排序规则是通过Comparator或Comparable接口来实现的。当构建TreeMap时，可以传入一个Comparator对象来指定比较规则，或者使用键对象实现Comparable接口来定义比较规则。以下是详细说明：

1. Comparator接口：Comparator接口是一个函数式接口，定义了一个用于比较两个对象的compare方法。在构建TreeMap时，可以传入一个Comparator对象来指定比较规则。Comparator接口的compare方法返回一个整数值，表示两个对象的比较结果。如果返回负数，则表示第一个对象小于第二个对象；如果返回正数，则表示第一个对象大于第二个对象；如果返回0，则表示两个对象相等。

示例代码如下：

```java
import java.util.Comparator;
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        Comparator<Person> nameComparator = new Comparator<Person>() {
            @Override
            public int compare(Person o1, Person o2) {
                return o1.name.compareTo(o2.name); // 按照姓名升序排序
            }
        };

        Comparator<Person> ageComparator = new Comparator<Person>() {
            @Override
            public int compare(Person o1, Person o2) {
                return o1.age - o2.age; // 按照年龄升序排序
            }
        };

        TreeMap<Person, Integer> treeMap1 = new TreeMap<>(nameComparator);
        treeMap1.put(new Person("Alice", 20), 90);
        treeMap1.put(new Person("Bob", 18), 80);
        treeMap1.put(new Person("Charlie", 22), 95);

        System.out.println("TreeMap1: " + treeMap1);

        TreeMap<Person, Integer> treeMap2 = new TreeMap<>(ageComparator);
        treeMap2.put(new Person("Alice", 20), 90);
        treeMap2.put(new Person("Bob", 18), 80);
        treeMap2.put(new Person("Charlie", 22), 95);

        System.out.println("TreeMap2: " + treeMap2);
    }
}
```

输出结果为：
```
TreeMap1: {Person{name='Alice', age=20}=90, Person{name='Bob', age=18}=80, Person{name='Charlie', age=22}=95}
TreeMap2: {Person{name='Bob', age=18}=80, Person{name='Alice', age=20}=90, Person{name='Charlie', age=22}=95}
```

在这个例子中，我们定义了两个Comparator对象，一个按照姓名升序排序，另一个按照年龄升序排序。然后，我们分别使用这两个Comparator对象创建了两个TreeMap对象，并存储了相同的键值对。通过输出结果可以看到，TreeMap根据不同的Comparator对象实现了不同的排序规则。
2. Comparable接口：Comparable接口是一个泛型接口，定义了一个用于比较对象的compareTo方法。如果键对象实现了Comparable接口，那么TreeMap会使用键对象的compareTo方法来进行比较排序。compareTo方法返回一个整数值，表示当前对象与另一个对象的比较结果。如果返回负数，则表示当前对象小于另一个对象；如果返回正数，则表示当前对象大于另一个对象；如果返回0，则表示两个对象相等。

示例代码如下：

```java
import java.util.TreeMap;

public class TreeMapExample {
    static class Student implements Comparable<Student> {
        private int age;
        private String name;

        public Student(int age, String name) {
            this.age = age;
            this.name = name;
        }

        @Override
        public int compareTo(Student o) {
            return this.age - o.age; // 按照年龄升序排序
        }

        @Override
        public String toString() {
            return "Student{" +
                    "age=" + age +
                    ", name='" + name + '\'' +
                    '}';
        }
    }

    public static void main(String[] args) {
        TreeMap<Student, Integer> treeMap = new TreeMap<>();
        treeMap.put(new Student(20, "Alice"), 90);
        treeMap.put(new Student(18, "Bob"), 80);
        treeMap.put(new Student(22, "Charlie"), 95);

        System.out.println("TreeMap: " + treeMap);
    }
}
```

输出结果为：

```
TreeMap: {Student{age=18, name='Bob'}=80, Student{age=20, name='Alice'}=90, Student{age=22, name='Charlie'}=95}
```

在这个例子中，我们定义了一个Student类，实现了Comparable接口，并重写了compareTo方法来实现按照年龄升序排序。然后，我们创建了一个TreeMap对象，并将Student对象作为键，整数作为值存储在TreeMap中。通过输出结果可以看到，TreeMap按照年龄升序排序存储键值对。

需要注意的是，如果键对象既实现了Comparable接口，又传入了Comparator对象，那么Comparator对象的比较规则会覆盖Comparable接口的比较规则。

1. 当⽐较规则不会发⽣改变的时候，或者说⽐较规则只有⼀个的时候，建议实现 Comparable 接口
2. 当⽐较规则有多个，并且需要在多个⽐较规则之间频繁切换时，建议使⽤ Comparator 接口



### 28. ConcurrentHashMap和Hashtable的key为什么都不能为空？HashMap的key可以为空？

Hashtable和HashMap都是基于哈希表实现的数据结构，但是它们在处理空键和空值的方式上有所不同。
Hashtable要求键和值都不能为空，因为在Hashtable内部，当插入一个键值对时，它会根据键的哈希码计算出一个索引，然后将该键值对存储在对应的索引位置上。如果键或值为空，那么无法计算出哈希码，也就无法确定键值对应该存储在哈希表的哪个位置上，因此会抛出NullPointerException异常。
而HashMap允许键为空。当插入一个键值对时，HashMap也会计算出一个索引，然后将该键值对存储在对应的索引位置上。如果键为空，HashMap会将该键值对存储在哈希表的第一个位置上，也就是索引为0的位置上。这样做的好处是，即使键为空，也不会影响其他键值对的存储和查找。
需要注意的是，虽然HashMap允许键为空，但是在使用时应尽量避免使用空键，因为这会影响哈希表的性能和效率。在Java 8中，HashMap的实现对空键做了优化，将空键存储在哈希表的第一个位置上，但是这样做会使得哈希表的链表变长，降低哈希表的性能。因此，如果键可能为空，建议使用Optional类来封装键，避免使用空键。

### 29. ConcurrentHashMap和Hashtable的value为什么都不能为空？HashMap的value可以为空？

参考：https://blog.csdn.net/cy973071263/article/details/126354336

ConcurrentHashMap允许插入 null（空） 值，那么，我们取值的时候会出现两种结果：

值没有在集合中，所以返回的结果就是 null （空）；
值就是 null（空），所以返回的结果就是它原本的 null（空） 值。



### 30. TreeMap和HashMap有什么区别？HashMap和Hashtable有什么区别？


TreeMap和HashMap的区别：

1. 排序：TreeMap是有序的键值对集合，它根据键的自然顺序或自定义的Comparator进行排序。而HashMap则是无序的键值对集合，不会对键进行排序。

2. 性能：HashMap的插入、删除和查找操作的时间复杂度都是O(1)，而TreeMap的插入、删除和查找操作的时间复杂度是O(logN)，其中N是键值对的数量。因此，在性能方面，HashMap通常比TreeMap更快。

3. 空间占用：TreeMap需要额外的空间来存储键的排序信息，因此它的空间占用比HashMap更大。

4. 迭代顺序：TreeMap的迭代顺序是按照键的顺序进行的，而HashMap的迭代顺序是不确定的。

5. 内部实现：TreeMap是基于红黑树的，HashMap是基于哈希表+红黑树的

HashMap和Hashtable的区别：

1. 线程安全性：Hashtable是线程安全的，而HashMap是非线程安全的。Hashtable的方法都是同步的，可以在多线程环境下使用，但是会影响性能。而HashMap没有进行同步处理，不是线程安全的，如果在多线程环境下使用，需要手动进行同步处理。

2. 允许空键和空值：HashMap允许键和值为空，而Hashtable不允许键和值为空。如果尝试将空键或空值放入Hashtable中，会抛出NullPointerException异常。

3. 继承关系：Hashtable是Dictionary类的子类，而HashMap是AbstractMap类的子类。

4. 初始容量和增长因子：Hashtable的初始容量和增长因子是固定的，而HashMap可以通过构造函数指定初始容量和增长因子，也可以根据需要进行动态调整。

总的来说，TreeMap适用于需要有序遍历的场景，HashMap适用于无序的快速查找和插入操作，Hashtable适用于多线程环境下的安全操作。

## ConcurrentHashMap

### 31. 什么时候扩容和转化为红黑树？
元素个数达到扩容阈值或链表长度达到扩容。
集合长度达到64，链表长度达到8时，链表转换为红黑树
### 32. 并发情况下，各线程中的数据可能不是最新的，那为什么 get 方法不需要加锁？
get 方法不需要加锁。因为 Node 的元素 value 和指针 next 是用 volatile 修饰的，在多线程环境下线程A修改节点的 value 或者新增节点的时候是对线程B可见的。
### 33. get 方法不需要加锁与 volatile 修饰的哈希桶数组有关吗？
没有关系。哈希桶数组table用 volatile 修饰主要是保证在数组扩容的时候保证可见性。
### 34. JDK1.8 中为什么使用内置锁 synchronized替换 可重入锁 ReentrantLock？
在 JDK1.6 中，对 synchronized 锁的实现引入了大量的优化，并且 synchronized 有多种锁状态，会从无锁 -> 偏向锁 -> 轻量级锁 -> 重量级锁一步步转换。
减少内存开销 。假设使用可重入锁来获得同步支持，那么每个节点都需要通过继承 AQS 来获得同步支持。但并不是每个节点都需要获得同步支持的，只有链表的头节点（红黑树的根节点）需要同步，这无疑带来了巨大内存浪费。
｜
### 35. ConcurrentHashMap 的并发度是什么？\
并发度可以理解为程序运行时能够同时更新 ConccurentHashMap且不产生锁竞争的最大线程数。在JDK1.7中，实际上就是ConcurrentHashMap中的分段锁个数，即Segment[]的数组长度，默认是16，这个值可以在构造函数中设置。
如果自己设置了并发度，ConcurrentHashMap 会使用大于等于该值的最小的2的幂指数作为实际并发度，也就是比如你设置的值是17，那么实际并发度是32。
如果并发度设置的过小，会带来严重的锁竞争问题；如果并发度设置的过大，原本位于同一个Segment内的访问会扩散到不同的Segment中，CPU cache命中率会下降，从而引起程序性能下降。
在JDK1.8中，已经摒弃了Segment的概念，选择了Node数组+链表+红黑树结构，并发度大小依赖于数组的大小。
｜
### 36. ConcurrentHashMap 迭代器是强一致性还是弱一致性？
与 HashMap 迭代器是强一致性不同，ConcurrentHashMap 迭代器是弱一致性。
ConcurrentHashMap 的迭代器创建后，就会按照哈希表结构遍历每个元素，但在遍历过程中，内部元素可能会发生变化，如果变化发生在已遍历过的部分，迭代器就不会反映出来，而如果变化发生在未遍历过的部分，迭代器就会发现并反映出来，这就是弱一致性
｜
### 37. JDK1.7 与 JDK1.8 中ConcurrentHashMap 的区别？
数据结构：取消了 Segment 分段锁的数据结构，取而代之的是数组+链表+红黑树的结构。
保证线程安全机制：JDK1.7 采用 Segment 的分段锁机制实现线程安全，其中 Segment 继承自 ReentrantLock 。JDK1.8 采用CAS+synchronized保证线程安全。
锁的粒度：JDK1.7 是对需要进行数据操作的 Segment 加锁，JDK1.8 调整为对每个数组元素加锁（Node）。
链表转化为红黑树：定位节点的 hash 算法简化会带来弊端，hash 冲突加剧，因此在链表节点数量大于 8（且数据总量大于等于 64）时，会将链表转化为红黑树进行存储。
查询时间复杂度：从 JDK1.7的遍历链表O(n)， JDK1.8 变成遍历红黑树O(logN)。
｜
### 38. ConcurrentHashMap 和 Hashtable 的效率哪个更高？为什么？
ConcurrentHashMap 的效率要高于 Hashtable，因为 Hashtable 给整个哈希表加了一把大锁从而实现线程安全。而ConcurrentHashMap 的锁粒度更低，在 JDK1.7 中采用分段锁实现线程安全，在 JDK1.8 中采用CAS+synchronized实现线程安全。
### 39. 多线程下安全的操作 map还有其他方法吗？
还可以使用Collections.synchronizedMap方法，对方法进行加同步锁。
### 40. 多线程如何参与一起扩容？
流程如下：
根据操作系统的 CPU 核数和集合 length 计算每个核一轮处理桶的个数，最小是16.

修改 transferIndex 标志位，每个线程领取完任务就减去多少，比如初始大小是transferIndex = table.length = 64，每个线程领取的桶个数是16，第一个线程领取完任务后transferIndex = 48，也就是说第二个线程这时进来是从第 48 个桶开始处理，再减去16，依次类推，这就是多线程协作处理的原理

领取完任务之后就开始处理，如果桶为空就设置为 ForwardingNode ,如果不为空就加锁拷贝，只有这里用到了 synchronized 关键字来加锁，为了防止拷贝的过程有其他线程在put元素进来。拷贝完成之后也设置为 ForwardingNode节点。

如果某个线程分配的桶处理完了之后，再去申请，发现 transferIndex = 0，这个时候就说明所有的桶都领取完了，但是别的线程领取任务之后有没有处理完并不知道，该线程会将 sizeCtl 的值减1，然后判断是不是所有线程都退出了，如果还有线程在处理，就退出
直到最后一个线程处理完，发现 sizeCtl = rs<< RESIZE_STAMP_SHIFT 也就是标识符左移 16 位，才会将旧数组干掉，用新数组覆盖，并且会重新设置 sizeCtl 为新数组的扩容点。

以上过程总的来说分成两个部分：
分配任务：这部分其实很简单，就是把一个大的数组给切分，切分多个小份，然后每个线程处理其中每一小份，当然可能就只有1个或者几个线程在扩容，那就一轮一轮的处理，一轮处理一份
处理任务：复制部分主要有两点，第一点就是加锁，第二点就是处理完之后置为ForwardingNode来占位标识这个位置被迁移过了。

