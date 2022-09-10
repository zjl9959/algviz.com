---
layout: page
title:  "关于 Algviz"
date:   2022-08-22 20:30:12 +0800
categories: help
comments: false
lang: zh
---

## 基本介绍

Algviz 是一个用于生成算法可视化动画的 Python 库，它可以和 [Jupyter-notebook](https://jupyter.org/) 很好的集成在一起。

Algviz 支持的数据结构十分丰富，它可以为向量 (`vector`)、表格 (`table`)、链表 (`linked list`)、树 (`tree`)、拓扑图(`graph`) 等数据结构生成可视化的动画。你只需要在你的 Python 代码中插入一些 algviz 相关的[接口](https://algviz.readthedocs.io/en/latest/api.html#module-algviz)，便可以轻松的在你的 Jupyter-notebook 中观看这些数据结构的变化过程。例如，下面的动画就展示了一个使用 algviz 进行可视化的[冒泡排序算法](https://en.wikipedia.org/wiki/Bubble_sort):

![bubble_sort_animation](https://cdn.jsdelivr.net/gh/zjl9959/algviz@main/docs/animation_images/bubble_sort.svg)

如果你想出来了一个很棒的算法，却不知道如何向你的朋友讲清楚它是怎么运行的，那么此时的你可以使用 algviz 去创建一个简单的演示动画。你不用担心这一过程太复杂，也不用去了解动画更新的原理，你需要做的只是如何去实现你的算法，剩下的交给 algviz 就好！
举个例子，一个[二叉树的镜像算法](https://medium.com/@ajinkyajawale/convert-a-binary-tree-into-its-mirror-tree-42ea44cea237)中包含对二叉树的递归操作，所以我们很难去想象：哪个树节点先被访问到？树的结构在何时会被修改？…… 但是 algviz 能够将这一复杂的过程通过直观的动画展现出来，就像下面的动画这样：

![mirror_tree_animation](https://cdn.jsdelivr.net/gh/zjl9959/algviz@main/docs/animation_images/mirror_tree_complete.svg)

你不必担心使用 algviz 的学习成本，因为它提供的大部分接口都和 Python 自带的内置类 (built-in class) 很相似。例如，你可以用下面的方式对一个 algviz 向量对象 [algviz.Vector](https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector) 进行遍历，就像去遍历一个 Python list 对象一样：

```python
import algviz                   # 导入 algviz 库。
viz = algviz.Visualizer()       # 创建一个可视化容器。
data = [1, 2, 3]
vector = viz.createVector(data) # 创建一个向量对象。
for num in vector:              # 对向量进行遍历，打印其中的每个值。
    print(num)
    viz.display()               # 这一步会刷新 Jupyter-notebook 中的显示动画。
```

这里解释一下例子中 [display](https://algviz.readthedocs.io/en/latest/api.html#algviz.visual.Visualizer.display) 接口的原理： algviz 会记录你对向量，表格，树等数据结构的各种操作，然后当你在下一次调用 `display` 接口时，它将这些操作合并到 “一帧” 动画序列中并输入到显示模块。所以在使用 algviz 时，你可能需要考虑一下：什么时候调用 `display` 接口是合适的？


## 安装步骤

### 第一步：安装 Jupyter-notebook

你可以选择以下任意一种方式进行安装：

+ 如果正在使用 [vscode](https://code.visualstudio.com/)，你可以直接安装 vscode 所提供的 Jupyter 拓展插件 [extension](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)。
+ 你可以参考 Jupyter-notebooks 官方提供的安装教程 [Install Jupyter](https://jupyter.org/install) 进行安装，并通过你的浏览器访问笔记。
+ 

### 第二步：安装 Graphviz

[Graphviz](https://graphviz.org/) 是一个十分流行的拓补图布局软件，你可以从它的[官网](https://graphviz.org/download/)进行下载安装。

*请注意：别忘了把 graphviz 的可执行文件所在路径添加到你的系统环境变量中去，这样 algviz 才能使用它！*

### 第三步：安装 algviz

通过 `pip` 下载安装即可，参考以下步骤：

```shell
python -m pip install --upgrade pip
pip install algviz
```

*请注意：algviz 需要运行在 Python 3.7 或者更高的版本上！*

## API 接口

你可以在 [readthedocs](https://algviz.readthedocs.io/en/latest/api.html#) 中找到关于 algviz 所有的 API 接口的介绍。

## 使用教程

你可以在 [examples](https://github.com/zjl9959/algviz/tree/main/examples) 文件夹中找到 algviz 的使用教程，但是在执行这些脚本之前，请参考前面的步骤配置好你的本地环境，否则可能会运行失败。

## 单元测试

你可以通过单元测试来验证本地配置环境的正确性，具体步骤如下：

1. 从 Github 下载单元测试[代码](https://github.com/zjl9959/algviz/tree/main/tests)；
2. 调用以下命令执行单元测试：
    ```shell
    python tests/run.py
    ```
3. 如果你看到了下面的执行结果：
    > Congratulations, everything is OK !!!
    
    那么你的本地配置环境一切正常，否则，你可以从[这里](https://github.com/zjl9959/algviz/issues)报告你的错误。

## 许可证

Algviz 使用 GNU GPLv3 [许可证](https://github.com/zjl9959/algviz/blob/main/LICENSE)，你可以免费的使用它进行学习和交流，但请不要将它用于商业活动！

## 相关链接

+ [algviz.com](https://algviz.com/)
+ [GitHub 项目地址](https://github.com/zjl9959/algviz)
+ [PyPi 主页](https://pypi.org/project/algviz/)
+ [API 接口介绍](https://algviz.readthedocs.io/en/latest/index.html)


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
