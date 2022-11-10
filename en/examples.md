---
layout: page
title:  "Tutorial"
date:   2022-10-27 20:22:16 +0800
comments: false
lang: en
---

This tutorial will teach you how to use Algviz for algorithm visualization programming. For the complete interface definition, please refer to the [Algviz API](https://algviz.readthedocs.io/en/latest/api.html) description document. The table below lists the Jupyter Notebook examples, you can try it by yourself.

| Example         |  Github link            | Google Colab link          |  Description                       |
| :----           | :------                 | :---------                 | :-------                           |
| **vector**      | [vector.ipynb]          | [vector.ipynb colab]       | Basic operations on [Vector] class. <br> Example of `bubble sort algorithm`. |
| **table**       | [table.ipynb]           | [table.ipynb colab]        | Basic operations on [Table] class.  |
| **linked list** | [linked_list.ipynb]     | [linked_list.ipynb colab]  | Create linked list and operate [ForwardLinkedNode], [DoublyLinkedNode] classes. |
| **tree**        | [tree.ipynb]            | [tree.ipynb colab]         | Create [binary tree], [normal tree] <br> Operate [TreeNode], [BinaryTreeNode] classes. <br> Example of `mirror binary tree`. <br> Example of construct `trie tree`. |
| **graph**       | [graph.ipynb]           | [graph.ipynb colab]        | Create [graph] and operate [GraphNode] class. |


## Visualizer

When using Algviz, the first object you should create is the [Visualizer](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer) object. Visualization objects are used to synchronize animation frames, control animation sequences, and manage each data object to be displayed.

### Create a visualizer object

When creating a visualizer object, you can specify the `delay` of each animation frame and the `wait` time between two adjacent animation frames.
*If you need to debug, you can set the `wait` parameter to `True`, so that the animation in Jupyter Notebook will pause until you enter a command to continue running.*

```python
import algviz
# Create a visualizer object.
# The default duration of each frame of animation is 3.0 seconds.
# The interval between two frames of animation is 0.5 seconds.
viz = algviz.Visualizer(delay=3.0, wait=0.5)
```

### Control animation display

When the [Visualizer.display](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.display) interface is called, Algviz will reflect all data object changes into the animation and display it in the Jupyter Notebook.

```python
viz.display()               # Display the firt animation frame.
# Do something...
viz.display(delay=2.0)      # Display the second animation frame.
```

### Create data object

A data object is also a basic data container in Algviz (eg: vector, tree, graph). When you modify the content in the data object, Algviz will record the data changes and reflect the changes in the animation. Before using these data objects, you need to create them through the interface provided in Visualizer. Let's learn how to create each data object!


## Vector
  
[Vector](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector) is a one-dimensional array container defined in Algviz. You can use a Vector object just like a `list` object in Python.

### Create a vector object

The interface [Visualizer.createVector](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createVector) is used to create a vector object. When creating a vector object, you can specify the initial data in the vector, the name of the vector object, the cell size, and whether to display subscripts. Here is an example:

```python
vec = viz.createVector(
    data = [0, 1, 2, 3],        # The initial data in Vector.
    name = "Vector",            # The display name of the Vector.
    cell_size = (40, 40),       # The cell (width, height) of the Vector.
    histogram = False,          # Whether to display as a histogram style.
    show_index = True           # Whether to display subscripts.
)
viz.display()
```
![Create Vector object](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector.svg)

### Modify vector elements

The elements in the vector can be accessed sequentially through the `for ... in ...` iterator, and the elements at the specified positions in the vector can be accessed or modified through the `[]` operator.

```python
sum = 0
# Accesse the vector elements sequentially through an iterator.
for val in vec:
    sum += val
vec[0] = sum
viz.display()
vec[0] -= 1
viz.display()
```

![example_vector_modify](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_modify.svg)

### Add elements to vector

+ The interface [Vector.append](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.append) is used to add a new element to the tail of the vector.
+ The interface [Vector.insert](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.insert) is used to insert a new element into the vector at the specified position.

```python
vec.append(0)               # Adds a new element 0 at the end of the vector.
viz.display()               # Render the first frame of animation.
vec.insert(index=4, val=4)  # Insert element 4 before the index position 4.
viz.display(3)              # Render the second frame of animation.
```

![example_vector_add](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_add.svg)

### Mark elements in vector

+ The interface [Vector.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.mark) can mark the specified element in the vector with the specified color.
*If the parameter `hold` is set to `True`, the marker will not be removed in subsequent animation frames, otherwise the marker will be automatically removed in the next animation frame.*
+ The interface [Vector.removeMark](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.removeMark) is used to remove the specified color mark from the vector.

```python
# Mark the element at position 3 in the vector green,
# the marker will be cleared on the next frame.
vec.mark(algviz.color_green, 3)
viz.display(1.0)
# All elements in the interval [0, 3) in the vector are marked as gray,
# the marker will not be cleared in later animation frames.
vec.mark(algviz.color_gray, st=1, ed=3, hold=True)
viz.display(1.0)
# Clear all gray marks.
vec.removeMark(algviz.color_gray)
viz.display(1.0)
```

![example_vector_mark](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_mark.svg)

### Swap elements position

The interface [Vector.swap](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.swap) can swap elements at two specified positions in the vector and generate the swap animation effects.

```python
# Swap the elements at position 0 and position 4.
vec.swap(0, 5)
viz.display(3.0)
```

![example_vector_swap](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_swap.svg)

### Delete elements in vector

+ The interface [Vector.pop](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.pop) removes the element at the specified position in the vector.
+ Interface [Vector.clear](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.clear) Clears all elements in a vector.

```python
vec.pop(index=2)    # Remove the element at index position 2.
viz.display(3)
vec.clear()         # Clears all elements in a vector.
viz.display(3)
```

![example_vector_remove](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_vector_remove.svg)

## Table

### Create a Table object

The interface [Visualizer.createTable](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createTable) is used to create a new table object.
When creating a table object, you must specify the rows and columns number of the table(you can adjust the rows and columns later). You can specify the initial data in the table, the name of the table, the length and width of the table cell, and whether to display row and column subscripts. Here is an example:

```python
tab = viz.createTable(
    row = 3,                    # The table has 3 rows.
    col = 3,                    # The table has 3 columns
    data = None,                # The initial data in table.
    name = "Table",             # The name of table.
    cell_size = (40, 40),       # The table cell (width, height).
    show_index = True           # Whether to display subscripts.
)
viz.display()
```

![example_table](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_table.svg)

### Modify table elements

You can access the elements in the table by the `for ... in ...` iterator. But unlike the `vector` object, you need two levels of nested `for ... in ...` to access specific elements in the table. The first level iterate on raws and the second level iterate on columns of each raw. Besides, you can also access the elements in the table through the `[raw][col]` operator.

```python
# Access all elements in the table through an iterator.
sum = 0
for row in tab:
    for val in row:
        sum += val
# Modify elements in the table with the "[]" operator.
tab[1][1] = sum
viz.display(0.5)
```

### Mark elements in table

+ The interface [Table.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.mark) can mark the specified element in the table with the given color.
*Similar to `Vector.mark`, if the parameter `hold` is set to `True`, the marker will not be removed in the later animation frames, otherwise, the marker will be automatically removed in the next frame;*
+ The interface [Table.removeMark](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.removeMark) is used to remove the specified color marks from the table.

```python
# Mark the element at (row:1, col:1) as green.
tab.mark(algviz.color_green, 1, 1)
viz.display(1)
tab.removeMark(algviz.color_green)
viz.display(1)
```

![example_table_mark](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_table_mark.svg)

### Adjust table shape

+ The interface [Table.shape](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.shape) is used to query the current shape of the table and the return value is `（row, column）`.
+ The interface [Table.reshape](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.reshape) is used to change table's shape. You can make a table become bigger or smaller.

```python
tab.reshape(row=2, col=2)  # Change the table shape to (row:2, col:2).
viz.display(1)
tab.reshape(row=2, col=3)  # Change the table shape to (row:2, col:3).
viz.display(1)
```

![example_table_reshape](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_table_reshape.svg)

-------------

Before learning the `linked list`, `tree` and `graph`, please review the `Vector` and `Table` introduced earlier. Since vectors and tables are sequential storage structures, you can directly access the elements in them through vector and table objects, but linked list, tree, and graph are relational storage structures, and you cannot directly access any of them through an entry. elements.

Firstly, you need to create a [SvgGraph](https://algviz.readthedocs.io/en/latest/api.html#algviz.svg_graph.SvgGraph) object through the interface [Visualizer.createGraph](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createGraph), you can learn how to use the `SvgGraph` later.

## linked list

### Create forward linked list

The `forward linked list` is connected by the [ForwardLinkedListNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.ForwardLinkedListNode) objects, which has a `val` member and a pointer point to the `next` node.

Algviz provides the [parseForwardLinkedList](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.parseForwardLinkedList) interface to create a `forward linked list`, so that there is no need to manually connect the `ForwardLinkedListNode` objects one by one.

```python
head1 = algviz.parseForwardLinkedList([0, 1, 2, 3])
forward_list = viz.createGraph(
    data = head1,
    name = 'Forward Linked List',
)
viz.display()
```

![example_forward_list](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_forward_list.svg)

### Create doubly linked list

The `doubly linked list` is constructed by the [DoublyLinkedListNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.DoublyLinkedListNode) nodes. The `DoublyLinkedListNode` has a `val` member, a pointer to the predecessor node `prev` and a pointer to the successor node `next`.

Similarly, Algviz provides the [parseDoublyLinkedList](https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.parseDoublyLinkedList) interface to create a `doubly linked list`, which **returns the first and last nodes of the doubly linked list**.

```python
head2, tail2 = algviz.parseDoublyLinkedList([0, 1, 2, 3])
doubly_list = viz.createGraph(
    data = head2,   # Just pass in the head node here.
    name = 'Doubly Linked List',
)
viz.display()
```

![example_doubly_list](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_doubly_list.svg)

### Modify linked list

When a node is added or deleted in the `linked list`, Algviz can automatically detect its change and generate corresponding animation.

```python
# Delete node 1.
head1_next = head1.next
head1.next = head1_next.next
forward_list.removeNode(head1_next)     # Remove the node from the SvgGraph.
viz.display()
# Add node 4.
forward_list_node = algviz.ForwardLinkedListNode(4, head1.next.next)
head1.next.next = forward_list_node
viz.display()
```

![example_linked_list_modify](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_linked_list_modify.svg)

*Tips: The [SvgGraph.removeNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.svg_graph.SvgGraph.removeNode) interface is used in the above code. This interface is used to delete an orphaned node from the topology graph, and the deleted node will not be showed in the animation.*

## Tree

### Create binary tree

The `binary tree` is connected by the [BinaryTreeNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.BinaryTreeNode). The `BinaryTreeNode` contains three members: the value[`val`] of the current node, the pointer[`left`] to the left subtree node and the pointer[`right`] to the right subtree node.

You can construct a binary tree manually, or you can construct a binary tree through the [parseBinaryTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseBinaryTree) interface.

```python
root1 = algviz.parseBinaryTree([1, 2, 3, 4, None, 5, 6])
binary_tree = viz.createGraph(data=root1, name='Binary Tree')
viz.display()
```

![example_binary_tree](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_binary_tree.svg)

### Modify binary tree

When tree nodes or relationships between nodes change, Algviz will automatically generate corresponding animations, for example:

```python
# Swap the left and right subtrees.
temp = root1.left
root1.left = root1.right
root1.right = temp
viz.display()
# Add a new node for tree node 2.
new_node = algviz.BinaryTreeNode('new')
root1.right.right = new_node
viz.display()
```

![example_binary_tree_modify](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_binary_tree_modify.svg)

### Create multi-child tree

Unlike a `binary tree`, each parent node of a `multi-child tree` may have multiple child nodes, so the [TreeNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode) contains a list of child nodes, and supports the following operations to modify its child node list:

+ [TreeNode.children](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode.children) access all child nodes in the child node list iteratively.
+ [TreeNode.childAt](https://algviz.readthedocs.io/en/0.1.7/api.html#algviz.tree.TreeNode.childAt)  returns the child node object at the given position in the child node list.
+ [TreeNode.childIndex](https://algviz.readthedocs.io/en/0.1.7/api.html#algviz.tree.TreeNode.childIndex) returns the index of the given node in the child nodes list.
+ [TreeNode.add](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode.add) adds a new child node into the child node list.
+ [TreeNode.remove](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode.remove) removes a child node from the child node list.
+ [TreeNode.removeAt](https://algviz.readthedocs.io/en/0.1.7/api.html#algviz.tree.TreeNode.removeAt) removes the child node at the given position in the child node list.

If you want to create a `multi-child tree`, you can create `TreeNode` one by one and then connect them, or you can use the [parseTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseTree) interface to create a multi-child tree. Here is an example:

```python
tree_info = {
    0: [1, 2, 3],   # Node0 has child nodes: 1, 2, 3.
    1: [4, 5],      # Node1 has child nodes: 4, 5.
    2: [6]          # Node2 has child node: 6.
}
nodes_label = {
    0: 'root',      # Set the display name of node0 as 'root'.
    3: 'n3'         # Set the display name of node3 as 'n3'.
}
root2 = algviz.parseTree(tree_info, nodes_label)
tree = viz.createGraph(data=root2, name="Tree")
viz.display()
```

![example_tree](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_tree.svg)

### Modify multi-child tree

```python
# Visit all the child nodes in root2 and mark them.
for child in root2.children():
    tree.markNode(algviz.color_red, child)
    viz.display(1.0)
tree_node3 = root2.childAt(2)           # Record node3.
tree_node3.add(algviz.TreeNode(8))      # Add a new node8 for node3.
viz.display()
tree_node3.add(algviz.TreeNode(7), 0)   # Add a new node7 for node3.
viz.display()
root2.removeAt(1)                       # Remove the subtree 'node2->node6' of the root node.
viz.display()
```

![example_tree_modify](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_tree_modify.svg)

### Recursive tree

The [RecursiveTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree) can be used to show the recursive process of your algorithm. Please refer to the blog for its usage:[Introduction to the RecursiveTree tool]({{ site.url }}/en/RecursiveTree/)。

## Graph

### Create graph

The topology graph is composed of [GraphNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode), which contains information such as the value of the node and the list of neighbor nodes. Algviz provides the [parseGraph](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.parseGraph) interface for quickly creating a topology graph.

The following examples show how to create a graph object:

```python
# Create two graph nodes n1, n2.
n1 = algviz.GraphNode(val = "n1")
n2 = algviz.GraphNode(val = "n2")
# Add two edges: (n1->n2, e1), (n2->n1, e2)
n1.add(node=n2, edge="e1")
n2.add(node=n1, edge="e2")
graph1 = viz.createGraph(
    data = [n1, n2],        # Bind the graph node into SvgGraph.
    name = "Graph_1",       # The name of the graph is 'Graph_1'.
    directed = True         # The graph is a directed graph.
)
viz.display()
```

![example_graph1](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_graph1.svg)


```python
graph_nodes = algviz.parseGraph(
    nodes = [0, 1, 2],      # Defines the node ID here (no duplicate values).
    edges = [
        (0, 1, 'a-b'),      # Node 0 points to node 1, the edge shown as 'a-b'.
        (1, 2, 'b-c'),      # Node 1 points to node 2, the edge shown as 'b-c'.
        (2, 0, 'c-a')       # Node 2 points to node 0, the edge shown as 'c-a'.
    ],
    nodes_label = {
        0: 'a',             # Node 0 shown as 'a'.
        1: 'b',             # Node 1 shown as 'b'.
        2: 'c'              # Node 2 shown as 'c'.
    },
    directed = True         # The graph is a directed graph.
)
graph2 = viz.createGraph(graph_nodes, "Graph_2", True)
viz.display()
```

![example_graph2](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_graph2.svg)

### Modify graph

When the graph is modified, Algviz will automatically adjust the layout of the graph and generate corresponding animations. These are the interfaces:

+ [GraphNode.neighbors](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.neighbors) iterate over all neighbor nodes.
+ [GraphNode.neighborAt](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.neighborAt) returns the node object at the index position in the neighbor list.
+ [GraphNode.neighborIndex](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.neighborIndex) returns the index position of the given node in the neighbor list.
+ [GraphNode.add](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.add) add or insert a neighbor node into the neighbor list.
+ [GraphNode.remove](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.remove) remove a neighbor node from the neighbor list.
+ [GraphNode.removeAt](https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode.removeAt) removes the node at the specified index position among the neighbor nodes.

Here is the example:

```python
graph_nodes[2].remove(graph_nodes[0])           # Remove the edge from node c to node a.
viz.display()
graph_node_d = algviz.GraphNode('d')            # Create new node d.
graph_nodes[1].add(graph_node_d, 'b-d', 0)      # Add an edge from node b to node d.
graph_node_d.add(graph_nodes[0], 'd-a')         # Add an edge from node d to node a.
viz.display()
```

![example_graph_modify](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_graph_modify.svg)

## Cursor

The [Cursor](https://algviz.readthedocs.io/en/latest/api.html#algviz.cursor.Cursor) object can be used to indicate an index position in a vector or table. When you access an element in a vector or table by the cursor, Algviz will automatically bind the cursor to the corresponding vector or table object, and display how cursor moves.

### Create a cursor object

The interface [Visualizer.createCursor](https://algviz.readthedocs.io/en/latest/api.html#algviz.Visualizer.createCursor) is used to create a cursor object, you can specify the initial position and name of the cursor when creating.

*Tips: The cursor position can only be an integer, other types of values are meaningless.*

```python
i = viz.createCursor(
    offset = 1,  # 光标的初始索引位置为 1
    name = "i"   # 光标的名称为 i
)
j = viz.createCursor(3, "j")
```

After the cursor is created, it does not appear in animations by default, only when you use the cursor to access elements in a vector or table,
The cursor's position is only displayed in the associated vector or table object.

In addition, Algviz also provides [Visualizer.cursorRange](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer.cursorRange) interface for batch creation of cursor objects, which is very useful when accessing elements iteratively.

### Update the cursor positon

Once you have the cursor object, you can use it as an integer and elements in vectors and tables can be accessed through the cursor.

The cursor object supports common arithmetic operations:

`+`, `-`, `*`, `//`, `%`, `+=`, `-=`, `*=`, `//=`, `%=`.

The comparison operations are also supported:

`>`, `<`, `>=`, `<=`, `==`, `!=`。

If you want to update the cursor position to any integer, you need to use the `<<` operator.

The following example demonstrates how to use the cursor object:

### Access vector element by cursor

Elements in a vector can be accessed by passing the cursor object as an argument to the vector's `[]` operator.

*Tips: A vector or table object can bind multiple cursor objects!*

```python
# Create a new vector object.
vec2 = viz.createVector([0, 1, 2, 3], "Vector2", show_index=True)
# Access the elements in the vector sequentially by the cursor i.
while i < len(vec2):
    vec2[j] = vec2[i] + 1
    viz.display(1.0)
    i += 1
    j -= 1
viz.display(1.0)
```

![example_cursor_vector](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_cursor_vector.svg)

### Access table element by cursor

```python
i << 0                      # Set the position of cursor i to 0.
(r, c) = tab.shape()        # The table object is created earlier.
while i < r:                # Access each row in the table iteratively.
    while j < c:            # Access each column in the table iteratively.
        tab[i][j] = 0       # Update the currently accessed element.
        viz.display(1.0)
        j += 1              # Cursor j moves to the next column.
    i += 1                  # Cursor i moves to the next row.
    j << 0                  # Cursor j moves to the first column.
    viz.display()
```

![example_cursor_table](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_cursor_table.svg)

## Miscellaneous

### Print logs

To print the log, firstly, you need to create a [Logger](https://algviz.readthedocs.io/en/latest/api.html#algviz.logger.Logger) object through the [Visualizer.createLogger](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer.createLogger) interface and set the maximum number of lines in the log during initialization. Then you can call the [Logger.write](https://algviz.readthedocs.io/en/latest/api.html#algviz.logger.Logger.write) interface to write the information to be displayed. If the number of currently displayed log lines exceeds the limit, the oldest log will be removed automatically.

In addition, you can clear the currently displayed log at any time by calling the interface [clear](https://algviz.readthedocs.io/en/latest/api.html#algviz.logger.Logger.clear). Here is an example of how to print logs:

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

### Color table

When you are calling interfaces such as [Vector.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector.mark), [Table.mark](https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table.mark), and [SvgGraph.markNode](https://algviz.readthedocs.io/en/latest/api.html#algviz.svg_graph.SvgGraph.markNode), you need to pass in a triple `(R, G, B)` representing the RGB color value. For convenience, Algviz provides some predefined color values (eg: `algviz.color_red`), the following is the color table:

![example_color_table](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/example_color_table.svg)


[Vector]: https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector
[Table]: https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table
[ForwardLinkedNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.ForwardLinkedListNode
[DoublyLinkedNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.DoublyLinkedListNode
[binary tree]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseBinaryTree
[normal tree]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseTree
[TreeNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode
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
