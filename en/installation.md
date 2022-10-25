---
layout: page
title:  "Installation Steps"
date:   2022-10-25 20:19:16 +0800
comments: false
lang: en
---

Before starting the installation, please check that your **Python version >=3.7**.
If not, please update your Python version!
After that please update your pip version to the latest version:

```shell
python -m pip install --upgrade pip
```

### Step1: Install Jupyter Notebook

You can choose any of the following ways to install:

#### Method One: Jupyter

Refer to the [official installation tutorial](https://jupyter.org/install) provided by Jupyter:

```shell
pip install jupyterlab
```
or
```shell
pip install notebook
```

#### Method Two: VSCode

Use the [Jupyter extension](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) provided by [VSCode](https://code.visualstudio.com/).

#### Method Three: Anaconda

Install [Anaconda](https://docs.anaconda.com/anaconda/install/index.html) and use the built-in Jupyter Notebook in it.

### Step2: Install Graphviz

You can download and install it for free from the official website of [Graphviz](https://graphviz.org/download/).

*<font color="#FF0000">Once installed, add the Graphviz executable path to your system's environment variables!</font>*

### Step3: Install Algviz

```shell
pip install algviz
```

------

## Installation Verification

To make sure you have successfully installed [algviz](https://pypi.org/project/algviz/),
you can download the [test codes](https://github.com/zjl9959/algviz/tree/main/tests) from Github.
Then call the command:

```shell
python tests/run.py
```

If you see the output like this:

> Congratulations, everything is OK !!!

It means algviz works fine in your environment.
But if you get any unexpected errors, please [report](https://github.com/zjl9959/algviz/issues) the bug.
