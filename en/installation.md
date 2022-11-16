---
layout: page
title:  "Installation Steps"
date:   2022-10-25 20:19:16 +0800
comments: false
lang: en
---

## Try algviz online

There are some websites that support running Jupyter Notebook online,
such as [Mybindler](https://mybinder.org/), [Google Colab](https://colab.research.google.com/), [Kaggle](https://www.kaggle.com/), and so on.
The table below lists some online Jupyter Notebook examples. You can click the notebook links in the table and try it in your browser.

| Example         |  MyBinder            | Google Colab          |  Description                       |
| :----           | :------                 | :---------                 | :-------                           |
| **vector**      | [vector.ipynb]          | [vector.ipynb colab]       | Basic operations on [Vector] class. <br> Example of `bubble sort algorithm`. |
| **table**       | [table.ipynb]           | [table.ipynb colab]        | Basic operations on [Table] class.  |
| **linked list** | [linked_list.ipynb]     | [linked_list.ipynb colab]  | Create linked list and operate [ForwardLinkedNode], [DoublyLinkedNode] classes. |
| **tree**        | [tree.ipynb]            | [tree.ipynb colab]         | Create [binary tree], [normal tree] <br> Operate [TreeNode], [BinaryTreeNode] classes. <br> Example of `mirror binary tree`. <br> Example of construct `trie tree`. |
| **graph**       | [graph.ipynb]           | [graph.ipynb colab]        | Create [graph] and operate [GraphNode] class. |


## Local installation

Before starting the installation, please check that your **Python version >=3.7**.
If not, please update your Python version!
After that please update your pip version to the latest version:

```shell
python -m pip install --upgrade pip
```

### Step1: Install Jupyter Notebook

You can choose any of the following ways to install:

#### Method one: Jupyter

Refer to the [official installation tutorial](https://jupyter.org/install) provided by Jupyter:

```shell
pip install jupyterlab
```
or
```shell
pip install notebook
```

#### Method two: VSCode

Use the [Jupyter extension](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) provided by [VSCode](https://code.visualstudio.com/).

#### Method three: Anaconda

Install [Anaconda](https://docs.anaconda.com/anaconda/install/index.html) and use the built-in Jupyter Notebook in it.

### Step2: Install Graphviz

You can download and install it for free from the official website of [Graphviz](https://graphviz.org/download/).

*<font color="#FF0000">Once installed, add the Graphviz executable path to your system's environment variables!</font>*

### Step3: Install Algviz

```shell
pip install algviz
```

------

## Installation verification

To make sure you have successfully installed algviz,
you can download the [test codes](https://github.com/zjl9959/algviz/tree/main/tests) from Github.
Then call the command:

```shell
python tests/run.py
```

If you see the output like this:

> Congratulations, everything is OK !!!

It means algviz works fine in your environment.
But if you get any unexpected errors, please [report](https://github.com/zjl9959/algviz/issues) the bug.

----

After the installation is complete, you can refer to the [tutorial]({{ site.url }}/en/examples) to learn how to use Algviz to animate your own algorithm!

[Vector]: https://algviz.readthedocs.io/en/latest/api.html#algviz.vector.Vector
[Table]: https://algviz.readthedocs.io/en/latest/api.html#algviz.table.Table
[ForwardLinkedNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.ForwardLinkedListNode
[DoublyLinkedNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.linked_list.DoublyLinkedListNode
[binary tree]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseBinaryTree
[normal tree]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.parseTree
[TreeNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.TreeNode
[graph]: https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.parseGraph
[GraphNode]: https://algviz.readthedocs.io/en/latest/api.html#algviz.graph.GraphNode
[vector.ipynb]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Fvector.ipynb
[table.ipynb]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Ftable.ipynb
[linked_list.ipynb]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Flinked_list.ipynb
[tree.ipynb]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Ftree.ipynb
[graph.ipynb]: https://mybinder.org/v2/gh/zjl9959/algviz/main?labpath=examples%2Fgraph.ipynb
[vector.ipynb colab]: https://colab.research.google.com/drive/1RgAoKbiSBXdSvBg65pwu9pJp5bQL1pCs?usp=sharing
[table.ipynb colab]: https://colab.research.google.com/drive/1GH6XgKDpUA2GKxiLm5tljp19wUvmnDxO?usp=sharing
[linked_list.ipynb colab]: https://colab.research.google.com/drive/1rsg-6irXzQODPi6DUZhtu-pKq_r55hwV?usp=sharing
[tree.ipynb colab]: https://colab.research.google.com/drive/138pnzwoS2vdhssZyTx-k5rwBQNb2Hi9N?usp=sharing
[graph.ipynb colab]: https://colab.research.google.com/drive/14hF30-N9VGBb5-vkERPuURvmnB9VspU9?usp=sharing
