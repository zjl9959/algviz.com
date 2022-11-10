---
layout: page
title:  "使用教程"
date:   2022-10-27 20:22:16 +0800
comments: false
lang: zh
---

本教程将教会您如何使用 Algviz 进行算法可视化编程，完整的接口定义请参考 [Algviz API](https://algviz.readthedocs.io/en/latest/api.html) 描述文档。下表列出了一些在 JupyterNotebook 中的使用例子作为参考：

| 对象         |  Github 链接            | Google Colab 链接          |   简介                      |
| :----           | :------                 | :---------                 | :-------                           |
| **[vector]**      | [vector.ipynb]          | [vector.ipynb colab]       | 向量对象的基础操作。 <br> 例如：`冒泡排序算法`。 |
| **[table]**       | [table.ipynb]           | [table.ipynb colab]        | 表格对象的基本操作。  |
| **[linked list]** | [linked_list.ipynb]     | [linked_list.ipynb colab]  | 使用单向链表和双向链表。 |
| **[tree]**        | [tree.ipynb]            | [tree.ipynb colab]         | 使用二叉树和多叉树。 <br> 例如：`二叉树镜像算法` 和 `构造字典树`。 |
| **[graph]**       | [graph.ipynb]           | [graph.ipynb colab]        | 使用拓扑图对象。 |


## 可视化对象

在使用 Algviz 时，您第一个要创建的对象就是可视化对象 [Visualizer](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer)。
可视化对象用来同步动画帧、控制每帧动画的时长，以及管理每一个要显示的数据对象。

### 创建可视化对象

在创建一个可视化对象时，可以为其指定默认的动画帧时长，以及相邻两帧动画的间隔时长。
*如果需要调试，可以将 `wait` 参数设置为 `True`，这样 Jupyter Notebook 中的动画就会暂停下来，直到输入继续运行的指令。*

```python
import algviz
# 创建可视化对象，默认每帧动画时长 3.0 秒钟，两帧动画间隔 0.5 秒。
viz = algviz.Visualizer(delay=3.0, wait=0.5)
```

### 控制动画刷新

当 [Visualizer.display](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.display) 接口被调用时，
Algviz 才会在 Notebook 中更新从上一帧到当前时刻所有的数据对象的变化过程，简称为更新动画帧。

```python
viz.display()               # 显示第一帧动画，帧时长为默认值 3.0 秒。
# 做一些事情……
viz.display(delay=2.0)      # 显示第二帧动画，帧时长为设定值 2.0 秒。
```

### 创建数据对象

一个数据对象也是 Algviz 中一个基本的数据容器（例如：向量、树、拓扑图），当您修改数据对象中的内容时，
Algviz 会记录它们的变化，并为不同的操作生成相应的动画。而在使用这些数据对象之前，需要通过 Visualizer 中提供的接口来创建它们，下面介绍各个数据对象的创建方式。


## 向量
  
向量 [Vector](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector) 是 Algviz 中定义的一维数组容器。您可以像使用 Python 中的 `list` 对象一样来使用 Vector 对象，下面是具体的使用方法：

### 创建向量对象

接口 [Visualizer.createVector](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createVector) 用来创建一个向量对象。在创建向量对象时，您可以指定向量中的初始数据、向量对象的名称、单元格的长宽以及是否显示行列下标。如果向量中的元素都是数字，您也可以用 `histogram` 参考控制是否以直方图的样式来显示向量。下面是一个例子：

```python
vec = viz.createVector(
    data = [0, 1, 2, 3],        # 向量中的初始化数据；
    name = "Vector",            # 向量的显示名称；
    cell_size = (40, 40),       # 向量中基本单元格的显示长宽；
    histogram = False,          # 是否以条形图的形式显示；
    show_index = True           # 是否显示下标数字；
)
viz.display()
```
![向量对象](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector.svg)

### 访问和修改元素

可以通过 `for ... in ...` 迭代器来按顺序依次访问向量中的元素，也可以通过 `[]` 操作符来访问或是修改向量中指定位置处的元素。

```python
sum = 0
# 通过迭代器依次访问向量中的元素。
for val in vec:
    sum += val
vec[0] = sum
viz.display()
vec[0] -= 1
viz.display()
```

![向量访问和修改元素](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_modify.svg)

### 添加元素

+ 接口 [Vector.append](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.append) 用来向向量的尾部添加一个新的元素；
+ 接口 [Vector.insert](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.insert) 用来向向量指定位置处插入一个新的元素。

```python
vec.append(0)               # 在向量尾部添加一个新元素 0。
viz.display()               # 渲染第一帧动画。
vec.insert(index=4, val=4)  # 在索引位置 4 处之前插入元素 4。
viz.display(3)              # 渲染第二帧动画。
```

![向量添加元素](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_add.svg)

### 标记元素

+ 接口 [Vector.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.mark) 可以将向量中的指定元素标记为指定的颜色。*如果将参数 `hold` 设置为 True，那么标记将不会在后面的动画帧中被移除，否则标记会在下一帧动画中被自动移除；*
+ 接口 [Vector.removeMark](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.removeMark) 用来将指定的颜色标记从向量中移除。

```python
vec.mark(algviz.color_green, 3)     # 将向量中位置 3 处的元素标记为绿色，标记将在下一帧被清除。
viz.display(1.0)                    # 第一帧动画，显示绿色标记。
# 标记向量中 [0, 3) 区间中的所有元素为灰色，标记不会在后面的动画帧中被清除。
vec.mark(algviz.color_gray, st=1, ed=3, hold=True)
viz.display(1.0)                    # 第二帧动画，显示灰色标记，并清除前一帧动画中不带 hold 属性的标记。
vec.removeMark(algviz.color_gray)   # 清除所有的灰色标记。
viz.display(1.0)                    # 第三帧动画，主动移除灰色标记。
```

![向量标记元素](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_mark.svg)

### 交换元素位置

接口 [Vector.swap](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.swap) 可以对向量中指定两个位置处的元素进行交换，并生成对应的动画效果。

```python
vec.swap(0, 5)      # 交换向量中位置0和位置4处的元素。
viz.display(3.0)
```

![向量交换元素位置](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_swap.svg)

### 删除元素

+ 接口 [Vector.pop](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.pop) 移除向量中指定位置处的元素；
+ 接口 [Vector.clear](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.clear) 清空向量中的所有元素。

```python
vec.pop(index=2)    # 删除索引位置 2 处的元素。
viz.display(3)
vec.clear()         # 清除向量中的所有元素。
viz.display(3)
```

![向量删除](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_remove.svg)

## 表格

### 创建表格对象

接口 [Visualizer.createTable](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createTable) 用来创建一个新的表格对象。在创建表格对象时，您必须要指定表格有多少行和多少列（后面也可以动态调整表格行列数），可以指定表格中的初始数据、表格对象的名称、单元格的长宽以及是否显示行列下标。下面是一个例子：

```python
tab = viz.createTable(
    row = 3,                    # 表格行数；
    col = 3,                    # 表格列数；
    data = None,                # 表格中的数据；
    name = "Table",             # 表格名称；
    cell_size = (40, 40),       # 单元格的长宽；
    show_index = True           # 是否显示下标数字；
)
viz.display()
```

![创建表格对象](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_table.svg)

### 访问和修改元素

可以通过 `for ... in ...` 迭代器访问表格中的元素，和向量不同的是，您需要两层嵌套的 `for ... in ...` 才能访问到表格中具体的元素，第一层对表格中的“行”进行迭代，第二层对“行”中的元素进行迭代。此外，也可以通过两次 `[]` 操作来访问表格中的元素，两个 `[]` 中的索引分别对应表格中的某一“行”和某一“列”。

```python
# 通过迭代器访问表格中的所有元素。
sum = 0
for row in tab:
    for val in row:
        sum += val
tab[1][1] = sum     # 通过"[]"操作符修改表格中的元素。
viz.display(0.5)
```

### 标记元素

+ 接口 [Tabel.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.mark) 可以将表格中的指定元素标记为指定的颜色。*和 `Vector.mark` 类似，如果将参数 `hold` 设置为 True，那么标记将不会在后面的动画帧中被移除，否则标记会在下一帧动画中被自动移除；*
+ 接口 [Table.removeMark](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.removeMark) 用来将指定的颜色标记从表格中移除。

```python
# 标记表格中第一行第一列的元素为绿色。
tab.mark(algviz.color_green, 1, 1)
viz.display(1)
tab.removeMark(algviz.color_green)
viz.display(1)
```

![表格标记元素](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_table_mark.svg)

### 调整表格形状

+ 接口 [Table.shape](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.shape) 用来查询表格的当前形状，既行数和列数，返回 `（row, column）`；
+ 接口 [Table.reshape](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.reshape) 用来修改表格的形状，可以将表格变大或变小。

```python
tab.reshape(row=2, col=2)  # 将表格形状改为 2x2。
viz.display(1)
tab.reshape(row=2, col=3)  # 将表格形状改为 2x3。
viz.display(1)
```

![调整表格形状](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_table_reshape.svg)

-------------

在介绍链表、树和拓扑图之前，请您先回顾一下前面介绍的向量和表格。由于向量和表格属于顺序型储存结构，因此可以直接通过向量和表格对象来访问其中的元素，但链表、树和拓扑图属于关系型储存结构，您无法通过某个入口来直接的访问其中的任意个元素。

为了方便的对链表、树和拓扑图中的元素进行操作，您首先需要通过接口 [Visualizer.createGraph](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createGraph) 创建一个拓扑图可视化对象，该接口的具体使用方法将在后面分别介绍。

## 链表

### 创建单向链表

单向链表通过单向链表节点 [ForwardLinkedListNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.ForwardLinkedListNode) 连接起来，节点中有一个值 `val` 和指向下一个节点的指针 `next`。

Algviz 中提供了 [parseForwardLinkedList](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.parseForwardLinkedList) 接口来创建单向链表，这样就不需要手动的一个个把单向链表节点连接起来了。

```python
head1 = algviz.parseForwardLinkedList([0, 1, 2, 3])
forward_list = viz.createGraph(
    data = head1,
    name = 'Forward Linked List',
)
viz.display()
```

![单向链表](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_forward_list.svg)

### 创建双向链表

双向链表通过双向链表节点 [DoublyLinkedListNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.DoublyLinkedListNode) 连接起来，节点中有一个值 `val`、一个指向前驱节点的指针 `prev` 和一个指向后继节点的指针 `next`。

同样的，Algviz 中提供了 [parseDoublyLinkedList](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.parseDoublyLinkedList) 接口来创建双向链表，该接口**返回双向列表的首尾两个节点**。

```python
head2, tail2 = algviz.parseDoublyLinkedList([0, 1, 2, 3])
doubly_list = viz.createGraph(
    data = head2,   # 这里传入链表的头节点就行了。
    name = 'Doubly Linked List',
)
viz.display()
```

![双向链表](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_doubly_list.svg)

### 修改链表

当链表中有节点的新增或是删除时，Algviz 可以自动检测到它的变化，并生成相应的动画。

```python
# 删除节点 1。
head1_next = head1.next
head1.next = head1_next.next
forward_list.removeNode(head1_next)     # 这里将节点从拓扑图中删除。
viz.display()
# 新增节点 4。
forward_list_node = algviz.ForwardLinkedListNode(4, head1.next.next)
head1.next.next = forward_list_node
viz.display()
```

![修改链表](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_linked_list_modify.svg)

*提示：上面的代码中用到了 [SvgGraph.removeNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.svg_graph.SvgGraph.removeNode) 接口，该接口的作用是将一个孤立的节点从拓扑图中删除，被删除的节点将不会在动画中显示。*

## 树

### 创建二叉树

二叉树通过二叉树节点 [BinaryTreeNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.BinaryTreeNode) 连接起来，二叉树节点中包含了当前节点的值 `val`、左子树节点对象 `left` 和右子树节点对象 `right` 这三个成员。

您可以手动的去构建二叉树，也可以通过 [parseBinaryTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseBinaryTree) 接口来构造一个二叉树。

```python
# 列表中是二叉树节点值按照层次顺序的排序结果，空的节点使用 None 来表示。
root1 = algviz.parseBinaryTree([1, 2, 3, 4, None, 5, 6])
binary_tree = viz.createGraph(data=root1, name='Binary Tree')
viz.display()
```

![二叉树](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_binary_tree.svg)

### 修改二叉树

当树节点或节点之间的关系发生变化时，Algviz 会自动生成对应的动画，例如：

```python
# 交换左右子树
temp = root1.left
root1.left = root1.right
root1.right = temp
viz.display()
# 节点 2 新增一个子节点
new_node = algviz.BinaryTreeNode('new')
root1.right.right = new_node
viz.display()
```

![修改二叉树](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_binary_tree_modify.svg)

### 创建多叉树

和二叉树不同，多叉树的每个父节点可能有多个子节点，所以多叉树节点 [TreeNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode) 中包含了一个用于保存子节点的列表，并且支持以下操作来修改其子节点列表：

+ [TreeNode.children](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode.children) 迭代访问子节点列表中所有的子节点；
+ [TreeNode.childAt](https://algviz.readthedocs.io/en/0.1.7/api.html#algviz.tree.TreeNode.childAt) 返回子节点列表中指定位置处的子节点对象；
+ [TreeNode.childIndex](https://algviz.readthedocs.io/en/0.1.7/api.html#algviz.tree.TreeNode.childIndex) 返回指定节点在子节点列表中的位置索引；
+ [TreeNode.add](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode.add) 新增一个子节点；
+ [TreeNode.remove](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode.remove) 移除一个子节点；
+ [TreeNode.removeAt](https://algviz.readthedocs.io/en/0.1.7/api.html#algviz.tree.TreeNode.removeAt) 移除子节点列表指定位置处的子节点。

如果您想创建一个多叉树，可以逐个创建树节点 `TreeNode` 然后将节点连接起来，也可以使用 [parseTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseTree) 接口来创建一个多叉树。
下面是一个创建多叉树的例子：

```python
tree_info = {
    0: [1, 2, 3],   # 节点 0 有三个子节点 1,2,3;
    1: [4, 5],      # 节点 1 有两个子节点 4,5;
    2: [6]          # 节点 2 有一个子节点 6。
}
nodes_label = {
    0: 'root',      # 将节点 0 命名为 root;
    3: 'n3'         # 将节点 3 命名为 n3。
}
root2 = algviz.parseTree(tree_info, nodes_label)
tree = viz.createGraph(data=root2, name="Tree")
viz.display()
```

![多叉树](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_tree.svg)

### 修改多叉树

```python
# 依次迭代所有子节点，并标记当前正在访问的子节点。
for child in root2.children():
    tree.markNode(algviz.color_red, child)
    viz.display(1.0)
tree_node3 = root2.childAt(2)           # 记录节点 3；
tree_node3.add(algviz.TreeNode(8))      # 节点 n3 新增一个子节点 8；
viz.display()
tree_node3.add(algviz.TreeNode(7), 0)   # 节点 n3 插入一个子节点 7；
viz.display()
root2.removeAt(1)                       # 根节点移除子树 2->6；
viz.display()
```

![修改多叉树](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_tree_modify.svg)

### 递归树

[递归树](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree)是一种特殊的用途多叉树，您可以用递归树来演示递归算法的运行过程，具体的使用方法可以参考博客：[递归算法分析工具 RecursiveTree 使用介绍]({{ site.url }}/cn/RecursiveTree/)。

## 拓扑图

### 创建拓扑图

拓扑图由拓扑图节点 [GraphNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode) 组成，一个拓扑图节点中包含了节点的值和邻居节点的列表等信息。为了方便您使用拓扑图，Algviz 中提供了 [parseGraph](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.parseGraph) 接口用于快速创建一个拓补图。

下面展示了一些创建拓扑图的例子：

#### 手动创建拓扑图

```python
# 创建两个拓扑图节点 n1,n2
n1 = algviz.GraphNode(val = "n1")
n2 = algviz.GraphNode(val = "n2")
# 添加两条边：（n1->n2,e1）,(n2->n1,e2)
n1.add(node=n2, edge="e1")
n2.add(node=n1, edge="e2")
graph1 = viz.createGraph(
    data = [n1, n2],        # 绑定拓扑图节点；
    name = "Graph_1",       # 拓扑图名称；
    directed = True         # 拓扑图为有向图。
)
viz.display()
```

![拓扑图一](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_graph1.svg)

#### 使用接口创建拓扑图

```python
graph_nodes = algviz.parseGraph(
    nodes = [0, 1, 2],      # 这里定义节点的 ID（不能有重复值）；
    edges = [
        (0, 1, 'a-b'),      # 节点 0 指向节点 1 的边，显示为 a-b；
        (1, 2, 'b-c'),      # 节点 1 指向节点 2 的边，显示为 b-c；
        (2, 0, 'c-a')       # 节点 2 指向节点 0 的边，显示为 c-a；
    ],
    nodes_label = {
        0: 'a',             # 节点 0 的显示名称为 a；
        1: 'b',             # 节点 1 的显示名称为 b；
        2: 'c'              # 节点 2 的显示名称为 c；
    },
    directed = True         # 拓扑图为有向图；
)
graph2 = viz.createGraph(graph_nodes, "Graph_2", True)
viz.display()
```

![拓扑图二](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_graph2.svg)

### 修改拓扑图

当修改拓扑图节点的邻居信息时，Algviz 会自动调整拓补图的布局，并生成相应的动画，具体的操作接口为：

+ [GraphNode.neighbors](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.neighbors) 迭代所有的邻居节点；
+ [GraphNode.neighborAt](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.neighborAt) 返回邻居列表中索引位置处的节点对象；
+ [GraphNode.neighborIndex](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.neighborIndex) 返回给定节点在邻居列表中的索引位置；
+ [GraphNode.add](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.add) 新增或插入一个邻居节点；
+ [GraphNode.remove](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.remove) 移除一个邻居节点；
+ [GraphNode.removeAt](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.removeAt) 移除邻居节点中指定索引位置处的节点。

下面看一些具体的例子：

```python
graph_nodes[2].remove(graph_nodes[0])           # 移除从节点 c 指向节点 a 的边；
viz.display()
graph_node_d = algviz.GraphNode('d')            # 新建节点 d；
graph_nodes[1].add(graph_node_d, 'b-d', 0)      # 添加一条从节点 b 指向节点 d 的边；
graph_node_d.add(graph_nodes[0], 'd-a')         # 添加一条从节点 d 指向节点 a 的边。
viz.display()
```

![修改拓扑图](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_graph_modify.svg)

## 光标

光标对象 [Cursor](https://algviz.readthedocs.io/en/latest/api.html#algviz.cursor.Cursor) 可以用来指示向量或表格中的索引位置。当您通过光标来访问向量或表格中的对象时，Algviz 会自动将光标和对应的向量或表格对象进行绑定，并且在其对应位置处的元素旁添加光标移动的动画。

### 创建光标对象

要使用光标，首先需要创建一个光标对象。接口 [Visualizer.createCursor](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createCursor) 用来创建一个光标对象，您在创建时可以指定光标的初始位置和名称。
（*注意，光标的位置只能是整数，其他类型的值是没有意义的。*）

```python
i = viz.createCursor(
    offset = 1,  # 光标的初始索引位置为 1
    name = "i"   # 光标的名称为 i
)
j = viz.createCursor(3, "j")
```

光标被创建之后，默认情况下是不会出现在动画中的，只有当您使用光标来访问向量或是表格中的元素时，
才会在相关向量或表格对象中显示光标的位置。

此外，Algviz 还提供了 [Visualizer.cursorRange](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer.cursorRange) 接口用于批量创建光标对象，这在迭代访问元素时十分有用。

### 更新光标位置

有了光标对象以后，您就可以把它当作一个整数来使用，
而且可以通过光标来访问向量和表格中的元素。

光标对象支持常见的算术运算操作：
`+`、`-`、`*`、`//`、`%`、`+=`、`-=`、`*=`、`//=`和`%=`，
同时也支持常用的比较操作：`>`、`<`、`>=`、`<=`、`==`和`!=`。

如果想要更新光标的位置到任意一个整数，那么需要使用 `<<` 操作符。
下面通过例子来演示如何使用光标对象：

### 访问向量中元素

直接将光标对象作为参数传给向量的 `[]` 操作符，即可访问向量中的元素。

*提示：一个向量或表格对象可以绑定多个光标对象！*

```python
# 创建一个新的向量对象
vec2 = viz.createVector([0, 1, 2, 3], "Vector2", show_index=True)
# 通过光标 i 依次访问向量中的元素
while i < len(vec2):
    vec2[j] = vec2[i] + 1
    viz.display(1.0)
    i += 1
    j -= 1
viz.display(1.0)
```

![光标访问向量中元素](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_cursor_vector.svg)

### 访问表格中元素

```python
i << 0                      # 将光标 i 的位置设置为 0
(r, c) = tab.shape()        # 使用前面创建的表格对象
while i < r:                # 迭代访问表格中的每一行
    while j < c:            # 迭代访问表格中的每一列
        tab[i][j] = 0       # 更新当前访问的元素
        viz.display(1.0)
        j += 1              # 光标 j 移动到下一列
    i += 1                  # 光标 i 移动到下一行
    j << 0                  # 光标 j 移动到第一列
    viz.display()
```

![光标访问表格中元素](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_cursor_table.svg)

## 其他

### 打印日志

Algviz 中提供了日志 [Logger](https://algviz.readthedocs.io/en/latest/api.html#algviz.logger.Logger) 对象，您可以把它看作一块滚动刷新的屏幕。

要打印日志，首先您需要创建一个日志对象 [Visualizer.createLogger](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer.createLogger) 并在初始化时设置好日志的最大行数，之后调用 [Logger.write](https://algviz.readthedocs.io/en/latest/api.html#algviz.logger.Logger.write) 接口向日志中写入要显示的信息。如果当前显示的日志行数超出给定的限制时，最早显示的日志会被自动移除掉。

此外，您也可以通过调用接口 [clear](https://algviz.readthedocs.io/en/latest/api.html#algviz.logger.Logger.clear) 随时清空当前显示的日志。下面是一个使用例子：

```python
log = viz.createLogger(3)
log.write('line1')
log.write('line2')
viz.display(1.0)
log.write('line3')
viz.display(1.0)
log.write('line4')
viz.display(1.0)
log.clear()
log.write('line5')
viz.display(1.0)
```

### 颜色对照表

在调用 [Vector.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.mark)、 [Table.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.mark) 以及 [SvgGraph.markNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.svg_graph.SvgGraph.markNode) 等接口时，您需要传入一个表示 RGB 颜色值的三元组。为了方便使用，Algviz 中提供了一些预定义的颜色值（如：`algviz.color_red`），下面是颜色对照表：

![颜色对照表](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_color_table.svg)

[Vector]: https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector
[Table]: https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table
[linked list]: https://algviz.readthedocs.io/en/latest/api.html#module-algviz.linked_list
[binary tree]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseBinaryTree
[tree]: https://algviz.readthedocs.io/en/latest/api.html#module-algviz.tree
[graph]: https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.parseGraph
[GraphNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode
[vector.ipynb]: https://github.com/zjl9959/algviz/blob/main/examples/vector.ipynb
[table.ipynb]: https://github.com/zjl9959/algviz/blob/main/examples/table.ipynb
[linked_list.ipynb]: https://github.com/zjl9959/algviz/blob/main/examples/linked_list.ipynb
[tree.ipynb]: https://github.com/zjl9959/algviz/blob/main/examples/tree.ipynb
[graph.ipynb]: https://github.com/zjl9959/algviz/blob/main/examples/graph.ipynb
[vector.ipynb colab]: https://colab.research.google.com/drive/1RgAoKbiSBXdSvBg65pwu9pJp5bQL1pCs?usp=sharing
[table.ipynb colab]: https://colab.research.google.com/drive/1GH6XgKDpUA2GKxiLm5tljp19wUvmnDxO?usp=sharing
[linked_list.ipynb colab]: https://colab.research.google.com/drive/1rsg-6irXzQODPi6DUZhtu-pKq_r55hwV?usp=sharing
[tree.ipynb colab]: https://colab.research.google.com/drive/138pnzwoS2vdhssZyTx-k5rwBQNb2Hi9N?usp=sharing
[graph.ipynb colab]: https://colab.research.google.com/drive/14hF30-N9VGBb5-vkERPuURvmnB9VspU9?usp=sharing
