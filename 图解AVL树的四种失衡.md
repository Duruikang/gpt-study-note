AVL 树在插入节点后，如果某个节点的**左右子树高度差 > 1**，就会发生失衡，需要通过**旋转（Rotation）**恢复平衡。

AVL 的四种经典失衡类型：

> LL、RR、LR、RL

可以记忆为：

```text
看失衡节点的“重方向”
```

---

# 1️⃣ LL 型（左左失衡） → 右旋

![Image](https://pages.cs.wisc.edu/~qingyi/Ratation.png)

![Image](https://www.freecodecamp.org/news/content/images/2020/02/avl_left_rotation.jpg)

## 出现场景

新节点插入在：

```text
左子树的左子树
```

示例：

插入 10 → 5 → 2

```text
      10
     /
    5
   /
  2
```

节点 10 失衡。

## 调整方法：右旋

```text
右旋后：

      5
     / \
    2   10
```

口诀：

```text
左左失衡 → 右旋
```

---

# 2️⃣ RR 型（右右失衡） → 左旋

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fwgo6zi51qz9mur74r6rr.png)

![Image](https://raw.githubusercontent.com/HebleV/valet_parking/master/images/avl_right_rotation.jpg)

## 出现场景

新节点插入在：

```text
右子树的右子树
```

示例：

插入 10 → 15 → 20

```text
10
  \
   15
     \
      20
```

节点 10 失衡。

## 调整方法：左旋

```text
左旋后：

      15
     /  \
   10    20
```

口诀：

```text
右右失衡 → 左旋
```

---

# 3️⃣ LR 型（左右失衡） → 先左旋，再右旋

![Image](https://www.sahinarslan.tech/static/f7f0575dc62e3797b1585c5c47f28dfa/ec061/avl-tree-double-rotation-left-right-right-left.jpg)

![Image](https://raw.githubusercontent.com/HebleV/valet_parking/master/images/avl_right_rotation.jpg)

## 出现场景

新节点插入在：

```text
左子树的右子树
```

示例：

插入 10 → 5 → 8

```text
      10
     /
    5
     \
      8
```

节点 10 失衡。

## 调整步骤

### 第一步：对 5 左旋

```text
      10
     /
    8
   /
  5
```

### 第二步：对 10 右旋

```text
      8
     / \
    5   10
```

口诀：

```text
左右失衡 → 先左旋 → 再右旋
```

---

# 4️⃣ RL 型（右左失衡） → 先右旋，再左旋

![Image](https://www.sahinarslan.tech/static/f7f0575dc62e3797b1585c5c47f28dfa/ec061/avl-tree-double-rotation-left-right-right-left.jpg)

![Image](https://raw.githubusercontent.com/HebleV/valet_parking/master/images/avl_left_rotation.jpg)

## 出现场景

新节点插入在：

```text
右子树的左子树
```

示例：

插入 10 → 15 → 12

```text
10
  \
   15
   /
  12
```

节点 10 失衡。

## 调整步骤

### 第一步：对 15 右旋

```text
10
  \
   12
     \
      15
```

### 第二步：对 10 左旋

```text
      12
     /  \
   10    15
```

口诀：

```text
右左失衡 → 先右旋 → 再左旋
```

---

# 五、四种失衡总结表

| 类型 | 插入位置 | 调整方式    |
| -- | ---- | ------- |
| LL | 左的左  | 右旋      |
| RR | 右的右  | 左旋      |
| LR | 左的右  | 左旋 + 右旋 |
| RL | 右的左  | 右旋 + 左旋 |

---

# 六、终极记忆口诀

```text
LL → 右旋
RR → 左旋
LR → 先左后右
RL → 先右后左
```

或者：

```text
外侧单旋
内侧双旋
```

---

如果你愿意，我可以继续帮你整理：

* 左旋右旋动态过程
* AVL vs 红黑树对比图
* 面试常考二叉树结构总结
