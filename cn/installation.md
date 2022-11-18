---
layout: page
title:  "安装步骤"
date:   2022-10-25 20:19:16 +0800
comments: false
lang: zh
---

## 网页版体验

有一些网站支持在线运行 Jupyter Notebook，例如：
（[Mybindler](https://mybinder.org/) *[无需注册] [启动较慢]*）、
（[Google Colab](https://colab.research.google.com/) *[需要注册]*）、
（[Kaggle](https://www.kaggle.com/) *[需要注册]*）等网站。
您可以点击下面的笔记链接，免安装直接体验 algviz 的强大功能！

| 对象         |  MyBinder        |  Kaggle     | Google Colab          |   简介                      |
| :----           | :------        | :-------         | :---------                 | :-------                           |
| **[vector]**      | [vector.ipynb binder]    |    [vector.ipynb kaggle]     | [vector.ipynb colab]       | 向量对象的基础操作。 <br> 例如：`冒泡排序算法`。 |
| **[table]**       | [table.ipynb binder]     |    [table.ipynb kaggle]     | [table.ipynb colab]        | 表格对象的基本操作。  |
| **[linked list]** | [linked_list.ipynb binder]  |  [linked_list.ipynb kaggle]    | [linked_list.ipynb colab]  | 使用单向链表和双向链表。 |
| **[tree]**        | [tree.ipynb binder]      |     [tree.ipynb kaggle]     | [tree.ipynb colab]         | 使用二叉树和多叉树。 <br> 例如：`二叉树镜像算法` 和 `构造字典树`。 |
| **[graph]**       | [graph.ipynb binder]     |    [graph.ipynb kaggle]     | [graph.ipynb colab]        | 使用拓扑图对象。 |

## 本地安装

在开始安装之前，请先**检查您的 Python 版本号是否大于等于 3.7**。
如果小于的话，请更新您的 Python 版本！
之后请更新您的 pip 版本至最新版：

```shell
python -m pip install --upgrade pip
```

### 第一步：安装 Jupyter Notebook

您可以选择以下任意一种方式进行安装：

#### 方式一：Jupyter

参考 Jupyter 官方提供的 [安装教程](https://jupyter.org/install)：

```shell
pip install jupyterlab
```
或是
```shell
pip install notebook
```

#### 方式二：VSCode

使用 [VSCode](https://code.visualstudio.com/) 提供的 [Jupyter 拓展插件](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)。

#### 方式三：Anaconda

安装 [Anaconda](https://docs.anaconda.com/anaconda/install/index.html)，使用其自带的 Jupyter Notebook。

### 第二步：安装 Graphviz

您可以直接从 [Graphviz](https://graphviz.org/download/) 的官方网站免费下载安装。

*<font color="#FF0000">安装完成后，请将 Graphviz 的可执行文件路径添加到系统的环境变量中！</font>*

### 第三步：安装 Algviz

```shell
pip install algviz
```

------

## 安装验证

要验证 algviz 是否安装成功，您可以从 Github 下载单元测试[代码](https://github.com/zjl9959/algviz/tree/main/tests)，然后执行命令：

```shell
python tests/run.py
```

如果您看到了下面的执行结果：

> Congratulations, everything is OK !!!

那么您的本地配置环境一切正常，否则，您可以从[这里](https://github.com/zjl9959/algviz/issues)报告您的错误。


----

安装完成之后，您可以参考[使用教程]({{ site.url }}/cn/examples)来学习如何使用 Algviz 让自己的算法动起来！


[Vector]: https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector
[Table]: https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table
[linked list]: https://algviz.readthedocs.io/en/latest/api.html#module-algviz.linked_list
[binary tree]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseBinaryTree
[tree]: https://algviz.readthedocs.io/en/latest/api.html#module-algviz.tree
[graph]: https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.parseGraph
[GraphNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode
[vector.ipynb binder]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Fvector.ipynb
[table.ipynb binder]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Ftable.ipynb
[linked_list.ipynb binder]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Flinked_list.ipynb
[tree.ipynb binder]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Ftree.ipynb
[graph.ipynb binder]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Fgraph.ipynb
[vector.ipynb kaggle]: https://www.kaggle.com/code/algviz/vector-example
[table.ipynb kaggle]: https://www.kaggle.com/algviz/table-example
[linked_list.ipynb kaggle]: https://www.kaggle.com/algviz/linked-list-example
[tree.ipynb kaggle]: https://www.kaggle.com/algviz/tree-example
[graph.ipynb kaggle]: https://www.kaggle.com/algviz/graph-example
[vector.ipynb colab]: https://colab.research.google.com/drive/1RgAoKbiSBXdSvBg65pwu9pJp5bQL1pCs?usp=sharing
[table.ipynb colab]: https://colab.research.google.com/drive/1GH6XgKDpUA2GKxiLm5tljp19wUvmnDxO?usp=sharing
[linked_list.ipynb colab]: https://colab.research.google.com/drive/1rsg-6irXzQODPi6DUZhtu-pKq_r55hwV?usp=sharing
[tree.ipynb colab]: https://colab.research.google.com/drive/138pnzwoS2vdhssZyTx-k5rwBQNb2Hi9N?usp=sharing
[graph.ipynb colab]: https://colab.research.google.com/drive/14hF30-N9VGBb5-vkERPuURvmnB9VspU9?usp=sharing
