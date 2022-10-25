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
