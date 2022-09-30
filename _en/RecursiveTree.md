---
layout: post
title:  "Introduction to the RecursiveTree tool"
date:   2022-09-29 5:28:00 +0800
categories: Tool Recursive
topmost: false
latex: false
lang: en
sec_svg: false
excerpt: Have you ever been confused by recursive algorithms? If so, don't miss the RecursiveTree class provided by algviz. You can easily see the recursive running process of the algorithm by simply calling the corresponding interface in the algorithm.
---

Have you ever been confused by recursive algorithms? If so, don't miss the RecursiveTree class provided by algviz. You can easily see the recursive running process of the algorithm by simply calling the corresponding interface in the algorithm.

## About RecursiveTree

RecursiveTree is a tree with multiply children in its node. Each node in the RecursiveTree represents a sub-problem to be solved by the recursive algorithm. The running process of the recursive algorithm is also the creation and traversal process of the RecursiveTree:

+ When the algorithm searches forward, a new child node will be added to the parent node, and the new child node will be marked in green;
+ When the algorithm backtracks, the node corresponding to the sub-problem will be marked in gray, and the node corresponding to the problem currently being processed will be marked in red.

We can intuitively see the running path of the recursive algorithm by the RecursiveTree. We can also get the recursion depth, breadth, and other information.

### API Reference

To use the RecursiveTree, we just need to do the following 3 steps:

1. **Initialization RecursiveTree**: create one [algviz.RecursiveTree](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree) object before the algorithm enters the recursive function body.
2. **Search forward**: call the [RecursiveTree.forward](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree.forward) interface at the entry of the recursive function, and pass in the name of the subproblem to solve.
3. **Search backward**: call the [RecursiveTree.backward](https://algviz.readthedocs.io/en/latest/api.html#algviz.tree.RecursiveTree.backward) interface at the exits of the recursive function.

## Example

### Fibonacci sequence problem

Usually, everyone comes into contact with the [Fibonacci sequence problem](https://www.mathsisfun.com/numbers/fibonacci-sequence.html) when learning recursive algorithms. Now let's take a look at how to use RecursiveTree to visualize the process of solving the Fibonacci sequence problem!

Firstly, let's take a look at the recursive solution algorithm for the Fibonacci sequence problem:

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

To visualize the algorithm, we just need to follow the above three steps to transform the algorithm. This is the code with RecursiveTree visualization:

```python
import algviz

viz = algviz.Visualizer()
name = "Fibonacci Recursive Tree"
tree = algviz.RecursiveTree(viz, name)  # 1. Create a RecursiveTree object.

def fib(n):
    tree.forward(n); viz.display()      # 2. Entrance.
    if n <= 1:
        tree.backward(); viz.display()  # 3.1 Exit 1.
        return n
    res = fib(n-1) + fib(n-2)
    tree.backward(); viz.display()      # 3.2 Exit 2.
    return res

print("fib(4)={}".format(fib(4)))
```

*Attention: When there are multiple exits in the recursive function, we need to call the `RecursiveTree.backward` interface at every exit.*

**The visualization animation is shown in the following figure:**

![RecursiveTree_Fibonacci](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/RecursiveTree_Fibonacci.svg)

## Supplementary Instructions

+ To use the RecursiveTree class, you need to install [algviz 0.1.6](https://pypi.org/project/algviz/0.1.6/) or higher version. For environment configuration, please refer to: [Installation](http://localhost:4000/en/about.html#installation).

+ *Algviz is an open source project, please give me a star on my [Github](https://github.com/zjl9959/algviz) if you are interested!*
