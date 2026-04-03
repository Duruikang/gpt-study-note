下面用**图解方式**详细讲清楚 **HashTable（哈希表）** 的结构、原理、冲突处理、时间复杂度，以及与 `HashMap` 的关系。

---

# 一、HashTable 是什么

**HashTable（哈希表）** 是一种：

> 根据 key 快速找到 value 的数据结构

核心思想：

```text
key  →  hash函数  →  数组下标  →  存储位置
```

查找效率通常：

```text
O(1)
```

非常快。

---

# 二、HashTable 基本结构

![Image](https://www.hello-algo.com/en/chapter_hashing/hash_map.assets/hash_function.png)

![Image](https://www.boardinfinity.com/blog/content/images/2023/03/HashMap-in-Python.png)

示例：

```text
key       hash(key)      index

Tom   →     3      →   table[3]
Lucy  →     7      →   table[7]
Jack  →     2      →   table[2]
```

底层：

```text
数组 + hash函数
```

例如：

```text
index: 0 1 2 3 4 5 6 7

           Jack  Tom        Lucy
```

---

# 三、hash函数的作用

hash函数用于：

```text
把 key 转换成数组下标
```

示例：

```text
hash("Tom") = 3
hash("Lucy") = 7
```

常见计算方式：

```text
index = hashCode(key) % 数组长度
```

例如：

```text
hashCode("Tom") = 123456
数组长度 = 10

index = 123456 % 10 = 6
```

存储位置：

```text
table[6]
```

---

# 四、哈希冲突（Hash Collision）

不同 key 可能得到相同 index：

```text
hash("Tom")  = 3
hash("Jack") = 3
```

发生冲突：

![Image](https://www.researchgate.net/publication/355070749/figure/fig1/AS%3A1076403399327748%401633645977759/llustration-of-a-classical-hash-map-using-separate-chaining-Keys-left-are-put-into.png)

![Image](https://miro.medium.com/1%2Al9eCykFTYwvLZgy62id5Ag.png)

必须解决冲突问题。

---

# 五、解决冲突的方法

主要两种：

---

# 1️⃣ 链表法（拉链法）

![Image](https://forns.lmu.build/assets/images/fall-2016/cmsi-281/week-14/hashtable-1.PNG)

![Image](https://www.researchgate.net/publication/355070749/figure/fig1/AS%3A1076403399327748%401633645977759/llustration-of-a-classical-hash-map-using-separate-chaining-Keys-left-are-put-into.png)

同一个位置存储一个链表：

```text
index 3:

Tom → Jack → Lucy
```

新元素直接加入链表。

优点：

* 实现简单
* 不容易满

缺点：

* 链表过长会变慢

时间复杂度：

```text
平均 O(1)
最坏 O(n)
```

---

# 2️⃣ 开放寻址法

![Image](https://labuladong.online/images/algo/ds-basic/hash-collision-en.jpeg)

![Image](https://www.mdpi.com/applsci/applsci-10-05218/article_deploy/html/images/applsci-10-05218-g001-550.jpg)

冲突时寻找下一个空位置：

```text
index 3 被占用

→ 试 index 4
→ 试 index 5
```

示例：

```text
index:

0 1 2 3 4 5 6

      Tom Jack
```

常见策略：

### 线性探测

一个一个往后找：

```text
+1 +2 +3
```

### 二次探测

```text
+1² +2² +3²
```

### 双重哈希

使用第二个 hash 函数。

---

# 六、HashTable 查找过程

查找 key：

```text
查找 Lucy
```

步骤：

```text
1️⃣ 计算 hash
2️⃣ 找到 index
3️⃣ 判断 key 是否相同
```

示例：

```text
hash("Lucy") = 7

直接访问：

table[7]
```

不需要遍历整个数据结构。

效率：

```text
O(1)
```

---

# 七、HashTable 时间复杂度

| 操作 | 时间复杂度 |
| -- | ----- |
| 查找 | O(1)  |
| 插入 | O(1)  |
| 删除 | O(1)  |

最坏情况：

```text
O(n)
```

例如：

所有 key 冲突：

```text
全部在一个链表中
```

---

# 八、HashTable vs HashMap

在 Java 中：

```text
HashTable
HashMap
```

区别：

| 对比        | HashTable | HashMap |
| --------- | --------- | ------- |
| 线程安全      | 是         | 否       |
| 性能        | 较慢        | 更快      |
| 是否允许 null | 不允许       | 允许      |
| 使用频率      | 较少        | 非常常用    |

现在开发中通常使用：

```text
HashMap
ConcurrentHashMap
```

---

# 九、HashMap 在 JDK8 的优化

当链表长度过长：

```text
> 8
```

链表转换为：

```text
红黑树
```

结构：

```text
数组 + 链表 + 红黑树
```

提升查询效率：

```text
O(n) → O(log n)
```

---

# 十、总结

HashTable 本质：

```text
数组 + hash函数
```

优点：

* 查询速度快
* 插入速度快
* 删除速度快

时间复杂度：

```text
O(1)
```

---

# 十一、一句话记忆

> HashTable 通过 hash函数把 key 映射到数组位置，从而实现快速查找。
---
<br><br><br><br>
下面用**图解 + 原理 + 面试要点**，系统讲清楚 **HashMap** 的底层结构与工作过程（基于 JDK 8）。

---

# 一、HashMap 是什么

**HashMap** 是一种：

> 存储 key-value（键值对）的数据结构
> 通过 key 快速找到 value

特点：

* 查询快
* 插入快
* 无序
* 允许一个 null key
* 非线程安全

时间复杂度（平均）：

```text
O(1)
```

---

# 二、HashMap 整体结构

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AhRQw_uorTsYsz2sNviPQYg.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AVv-mhn03QMIzVxEZkGpsew.png)

JDK8 中结构：

```text
数组 + 链表 + 红黑树
```

结构示例：

```text
index:

0   1   2   3   4   5   6   7

        key1
            ↓
          key2
            ↓
          key3
```

数组每个位置称为：

```text
bucket（桶）
```

---

# 三、HashMap 工作流程

插入：

```java
map.put("Tom",20);
```

执行步骤：

---

## 1️⃣ 计算 hash 值

调用：

```java
hashCode()
```

示例：

```text
hash("Tom") = 235436
```

---

## 2️⃣ 计算数组下标

公式：

```text
index = hash % 数组长度
```

例如：

```text
235436 % 16 = 12
```

存入：

```text
table[12]
```

---

## 3️⃣ 判断是否发生冲突

情况1：

该位置为空：

```text
直接存储
```

情况2：

已有元素：

```text
形成链表
```

示例：

```text
table[12]

Tom → Jack → Lucy
```

---

# 四、哈希冲突

不同 key 可能映射到同一位置：

```text
hash("Tom")  = 12
hash("Jack") = 12
```

结构：

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AV2N8-C5w8MiLoa760Wktzg.png)

![Image](https://miro.medium.com/1%2AnqrpEAWeV87VeN1zLQNTug.png)

解决方式：

```text
链表法（拉链法）
```

---

# 五、JDK8 优化：链表转红黑树

当链表过长：

```text
链表长度 > 8
```

转换为：

```text
红黑树
```

结构：

![Image](https://miro.medium.com/1%2AnqrpEAWeV87VeN1zLQNTug.png)

![Image](https://media.licdn.com/dms/image/v2/D4D22AQHX2TRuQtQclg/feedshare-shrink_1280/B4DZh8M72AHYAk-/0/1754430423329?e=2147483647\&t=54aUSLcgGaJo2we-MtNXcIA1OnIVQgjtbYoscFwb6_8\&v=beta)

查询效率提升：

```text
O(n) → O(log n)
```

条件：

```text
链表长度 ≥ 8
数组长度 ≥ 64
```

否则优先扩容。

---

# 六、HashMap 扩容机制（resize）

默认容量：

```text
16
```

负载因子：

```text
0.75
```

扩容条件：

```text
元素数量 > 容量 × 0.75
```

例如：

```text
16 × 0.75 = 12
```

当元素超过 12：

```text
扩容到 32
```

扩容过程：

```text
重新计算 index
重新分布元素
```

时间复杂度较高：

```text
O(n)
```

---

# 七、HashMap 查询流程

```java
map.get("Tom");
```

步骤：

```text
1️⃣ 计算 hash
2️⃣ 找到 bucket
3️⃣ 遍历链表或树
4️⃣ equals 比较 key
```

---

# 八、HashMap 时间复杂度

| 操作 | 时间复杂度 |
| -- | ----- |
| 查询 | O(1)  |
| 插入 | O(1)  |
| 删除 | O(1)  |

最坏：

```text
O(n)
```

JDK8 优化后：

```text
O(log n)
```

---

# 九、为什么 HashMap 快？

普通查找：

```text
遍历数组
O(n)
```

HashMap：

```text
直接定位位置
O(1)
```

核心优势：

```text
减少遍历次数
```

---

# 十、HashMap 重要特性

## 1️⃣ key 不能重复

```java
map.put("Tom",20);
map.put("Tom",30);
```

结果：

```text
Tom=30
```

旧值被覆盖。

---

## 2️⃣ 允许一个 null key

```java
map.put(null,10);
```

但：

```text
只能一个
```

---

## 3️⃣ key 需要重写 hashCode 和 equals

否则可能查找失败。

例如：

```java
class Person{
    String name;
}
```

必须重写：

```java
hashCode()
equals()
```

---

# 十一、HashMap vs Hashtable

| 对比   | HashMap | Hashtable |
| ---- | ------- | --------- |
| 线程安全 | 否       | 是         |
| 性能   | 快       | 慢         |
| null | 允许      | 不允许       |
| 推荐使用 | ✔       | ❌         |

线程安全版本：

```text
ConcurrentHashMap
```

---

# 十二、总结图

HashMap 本质：

```text
数组
  ↓
bucket
  ↓
链表
  ↓
红黑树（链表过长时）
```

---

# 十三、一句话总结

> HashMap 通过 hash函数把 key 映射到数组位置，冲突时使用链表或红黑树，从而实现高效查找。

---
<br><br><br><br>

**Bucket Array（桶数组）** 是 **HashMap / HashTable** 的核心底层结构。

一句话理解：

> **Bucket Array 就是用来存放数据的数组，每个数组位置叫一个 bucket（桶）。**

---

# 一、什么是 Bucket（桶）

在 HashMap 中：

数据不会直接按顺序存储，而是通过 hash 函数计算存储位置：

```text
key → hash函数 → 数组下标 → bucket
```

这个数组就是：

```text
Bucket Array
```

---

# 二、结构示意

![Image](https://miro.medium.com/1%2AjPbJs_q8IgrZjf1q8VsmSA.png)

![Image](https://i.sstatic.net/0yjYd.png)

示例：

```text
Bucket Array（数组）

index:

0
1
2 → (Tom,20)
3
4 → (Lucy,18)
5
6 → (Jack,25)
7
```

每一个 index：

```text
就是一个 bucket（桶）
```

---

# 三、为什么叫“桶”

因为每个位置可以存多个元素：

```text
bucket[3]:

Tom → Jack → Lucy
```

就像：

```text
一个桶里装多个东西
```

所以叫：

```text
bucket（桶）
```

---

# 四、JDK8 中 Bucket 的真实结构

在 HashMap 中：

```text
Node<K,V>[] table
```

就是 Bucket Array。

例如：

```java
Node[] table = new Node[16];
```

数组长度默认：

```text
16
```

结构：

```text
table[0]
table[1]
table[2]
...
table[15]
```

每个位置：

可能是：

```text
空
或
链表
或
红黑树
```

---

# 五、Bucket 内部结构

## 1️⃣ 无冲突

```text
bucket[5]:

(Tom,20)
```

---

## 2️⃣ 冲突 → 链表

```text
bucket[5]:

(Tom,20)
   ↓
(Jack,25)
   ↓
(Lucy,18)
```

---

## 3️⃣ 冲突过多 → 红黑树

```text
bucket[5]:

        Tom
       /   \
    Jack   Lucy
```

条件：

```text
链表长度 ≥ 8
```

---

# 六、完整结构

![Image](https://miro.medium.com/1%2AnqrpEAWeV87VeN1zLQNTug.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AVv-mhn03QMIzVxEZkGpsew.png)

整体：

```text
Bucket Array（数组）
        ↓
     bucket
        ↓
链表 / 红黑树
```

---

# 七、为什么需要 Bucket Array

如果不用 bucket：

查找数据：

```text
需要遍历整个集合
O(n)
```

有 bucket：

```text
直接定位位置
O(1)
```

性能大幅提高。

---

# 八、例子

```java
Map<String,Integer> map = new HashMap<>();

map.put("Tom",20);
map.put("Lucy",18);
map.put("Jack",25);
```

可能存储：

```text
bucket array:

index 2 → Tom
index 6 → Lucy
index 9 → Jack
```

通过：

```text
hashCode(key)
```

计算位置。

---

# 九、总结

Bucket Array：

```text
就是一个数组
用于存储数据的位置
```

每个 bucket：

```text
可以存：
一个节点
或链表
或红黑树
```

---

# 十、一句话记忆

> Bucket Array = HashMap 的底层数组，每个 bucket 是存储数据的位置。

---