---
layout: page
title:  "安装步骤"
date:   2022-10-25 20:19:16 +0800
comments: false
lang: zh
---

在开始安装之前，请先**检查您的 Python 版本号是否大于等于 3.7**。
如果小于的话，请更新您的 Python 版本！
之后请更新您的 pip 版本至最新版：

```shell
python -m pip install --upgrade pip
```

## 第一步：安装 Jupyter

您可以选择以下任意一种方式进行安装：

1. **官方版本**：参考 Jupyter 官方提供的 [安装教程](https://jupyter.org/install)：

    ```shell
    pip install jupyterlab
    ```
    或是
    ```shell
    pip install notebook
    ```

2. **VSCode 插件**：使用 [VSCode](https://code.visualstudio.com/) 提供的 [Jupyter 拓展插件](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)。

3. **Anaconda**：安装 [Anaconda](https://docs.anaconda.com/anaconda/install/index.html)，使用其自带的 Jupyter Notebook。

## 第二步：安装 Graphviz

您可以直接从 [Graphviz](https://graphviz.org/download/) 的官方网站免费下载安装。

*<font color="#FF0000">安装完成后，请将 Graphviz 的可执行文件路径添加到系统的环境变量中！</font>*

## 第三步：安装 Algviz

```shell
pip install algviz
```

*<font color="#FF0000">对于 Windows 用户，您需要额外安装 `pywin32` 库，请执行  `pip install pywin32` 命令！</font>*

------

## 【可选】安装验证

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
