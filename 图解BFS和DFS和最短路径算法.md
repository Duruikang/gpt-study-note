下面用**图解方式**理解 3 个核心算法：

* BFS（广度优先搜索）
* DFS（深度优先搜索）
* 最短路径算法（Shortest Path）

它们主要用于 **树 / 图（Graph）结构**。

---

# 一、BFS（广度优先搜索）

## 思想

> 一层一层向外扩展搜索

先访问距离起点最近的节点。

使用数据结构：

```text
队列（Queue）
```

---

## 图解

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AVM84VPcCQe0gSy44l9S5yA.jpeg)

![Image](https://deen3evddmddt.cloudfront.net/uploads/content-images/bfs-vs-dfs.webp)

示例图：

```text
        A
      /   \
     B     C
    / \   /
   D   E F
```

从 A 开始 BFS：

访问顺序：

```text
A
B C
D E F
```

结果：

```text
A → B → C → D → E → F
```

---

## BFS 执行过程

```text
队列变化：

[A]

取出 A → 加入 B C
[B C]

取出 B → 加入 D E
[C D E]

取出 C → 加入 F
[D E F]
```

---

## 时间复杂度

```text
O(V + E)
```

V = 顶点数
E = 边数

---

## 典型应用

* 最短路径（无权图）
* 社交关系距离
* 地图路径
* 层序遍历

---

# 二、DFS（深度优先搜索）

## 思想

> 一条路走到底，再回头

使用数据结构：

```text
栈（Stack）
或
递归
```

---

## 图解

![Image](https://he-s3.s3.amazonaws.com/media/uploads/9fa1119.jpg)

![Image](https://deen3evddmddt.cloudfront.net/uploads/content-images/bfs-vs-dfs.webp)

示例图：

```text
        A
      /   \
     B     C
    / \   /
   D   E F
```

DFS 访问顺序：

```text
A → B → D → E → C → F
```

过程：

```text
A
↓
B
↓
D
回退
E
回退
C
↓
F
```

---

## 时间复杂度

```text
O(V + E)
```

---

## 典型应用

* 路径搜索
* 拓扑排序
* 回溯算法
* 迷宫问题
* 连通性判断

---

# 三、BFS vs DFS 对比

| 对比       | BFS  | DFS    |
| -------- | ---- | ------ |
| 中文       | 广度优先 | 深度优先   |
| 搜索方式     | 一层一层 | 一条路走到底 |
| 数据结构     | 队列   | 栈 / 递归 |
| 是否能找最短路径 | ✔    | ❌      |
| 空间复杂度    | 较高   | 较低     |

---

# 四、最短路径算法

用于：

```text
找到两点之间最短距离
```

常见算法：

* BFS（无权图）
* Dijkstra（带权图）
* Floyd
* Bellman-Ford

---

# 五、最短路径图解（Dijkstra）

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AnXlEmHAnu3dVBOnJAfPaAg.jpeg)

![Image](https://www.researchgate.net/publication/380019273/figure/fig1/AS%3A11431281238545309%401713961927555/Example-of-a-simplified-graph-with-highlighted-shortest-path-between-node-A-and-node-F.png)

示例：

```text
A --1-- B --2-- D
 \      |
 4      3
  \     |
    C
```

求 A → D 最短路径：

可能路径：

```text
A → B → D = 1 + 2 = 3
A → C → B → D = 4 + 3 + 2 = 9
```

最短路径：

```text
A → B → D
距离 = 3
```

---

# 六、三种算法关系

```text
BFS / DFS → 图的遍历算法
最短路径 → 在遍历基础上计算距离
```

关系：

```text
BFS 可以求无权图最短路径
Dijkstra 求加权图最短路径
```

---

# 七、总结表

| 算法       | 作用   | 特点          |
| -------- | ---- | ----------- |
| BFS      | 按层搜索 | 可求最短路径（无权图） |
| DFS      | 深度搜索 | 常用于回溯       |
| Dijkstra | 最短路径 | 处理带权图       |

---

# 八、一句话记忆

```text
BFS：一层一层找
DFS：一条路走到底
最短路径：找距离最小路线
```

---

如果你愿意，我可以继续帮你整理：

* 邻接表 vs 邻接矩阵图解
* Dijkstra执行全过程图
* DFS回溯算法图解
