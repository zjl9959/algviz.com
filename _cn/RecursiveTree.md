---
layout: post
title:  "递归算法分析工具 RecursiveTree 使用介绍"
date:   2022-09-29 5:28:00 +0800
categories: 工具 递归
topmost: false
latex: false
lang: zh
sec_svg: false
excerpt: 大家是否有过被递归算法绕糊涂的经历呢？如果有的话，那请不要错过 algviz 提供的递归树对象（RecursiveTree）。只需在算法中简单的调用对应的接口，就可以方便的看到算法的递归运行过程。
---

大家是否有过被递归算法绕糊涂的经历呢？如果有的话，那请不要错过 algviz 提供的递归树对象（RecursiveTree）。只需在算法中简单的调用对应的接口，就可以方便的看到算法的递归运行过程。

## 关于递归树

递归树（RecursiveTree）是一颗多叉树，树中的每个节点代表递归算法要解决的一个子问题。递归算法的运行过程也是递归树的创建和遍历过程：
+ 当算法进行递归调用时，递归树中父问题对应的节点将会新增一个子节点，同时新增的子节点被标记为绿色；
+ 而当算法解决了一个子问题并进行回溯时，子问题对应的节点会被标记为灰色，同时当前正在处理的问题会被标记为红色。

通过递归树，我们可以直观的看到递归算法的运行路径，同时还可以了解到递归深度、广度等信息。

### 接口介绍

要使用递归树，我们只需要做以下3个步骤：

1. **创建递归树**：这一步只需要在算法**进入递归函数之前**创建一个 [algviz.RecursiveTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree) 对象即可；
2. **向前递归**：在递归函数的入口处调用 [RecursiveTree.forward](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree.forward) 接口并传入子问题的名称即可；
3. **向后回溯**：在递归函数的出口处调用 [RecursiveTree.backward](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree.backward) 接口即可。

## 使用说明

### 斐波那契数列

通常大家在学习递归算法时都会接触到[斐波那契数列问题](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/)，下面来看一下如何使用 RecursiveTree 来对斐波那契数列问题的求解过程进行可视化！

首先看一下斐波那契数列问题的递归求解算法：

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

要对算法进行可视化，我们只需要遵循上面三个步骤对算法进行改造即可。不多说了，直接看一下改造后的代码：

```python
import algviz

viz = algviz.Visualizer()
name = "Fibonacci Recursive Tree"
tree = algviz.RecursiveTree(viz, name)  # 1.创建递归树

def fib(n):
    tree.forward(n); viz.display()      # 2. 递归入口
    if n <= 1:
        tree.backward(); viz.display()  # 3.1 递归出口 1
        return n
    res = fib(n-1) + fib(n-2)
    tree.backward(); viz.display()      # 3.2 递归出口 2
    return res

print("fib(4)={}".format(fib(4)))
```

*注意：当递归函数中有多个出口时，需要在每个出口处都调用 `RecursiveTree.backward` 接口。*

**可视化后的动画如下图所示：**

![RecursiveTree_Fibonacci](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/RecursiveTree_Fibonacci.svg)

## 补充说明

+ 使用递归树（RecursiveTree），需要安装 [algviz 0.1.6](https://pypi.org/project/algviz/0.1.6/) 及以上的版本，环境配置请参考：[安装步骤](https://algviz.com/cn/about.html#%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)
+ *Algviz 是一个开源项目，感兴趣的朋友也可以去我的 [Github](https://github.com/zjl9959/algviz) 点一个 Star！*
