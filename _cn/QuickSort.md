---
layout: post
title:  "快速排序算法"
date:   2022-10-13 21:46:00 +0800
categories: 排序算法 递归
topmost: false
latex: true
lang: zh
sec_svg: true
excerpt: 快速排序算法最早由东尼·霍尔提出，又称分区交换排序算法，简称快排算法。快排算法在一般情况下的执行效率较高，在实际工程中有着广泛的应用。
---

快速排序算法最早由东尼·霍尔提出，又称**分区交换排序**算法，简称快排算法。快排算法在一般情况下的执行效率较高，在实际工程中有着广泛的应用。

## 算法思想

快排算法使用了**分治**的思想，这一点和[归并排序算法]({{ site.url }}/cn/MergeSort/)类似，不过快排算法使用了一种十分巧妙的方式来对子序列进行划分，而不是像归并排序算法那样简单的将序列从中间对半分开。
**快排算法将序列划分为左右两段，并保证左侧序列中最大的元素小于右侧序列中最小的元素。**为了实现这一点，快排算法从当前序列中挑选一个元素作为**基数**，并以基数为基准对序列进行分割，在分割时算法保证基数左边的子序列都小于基数，而基数右边的子序列都大于或等于基数。

## 算法实现

### 子序列分割

下面的动画展示了子序列的分割过程：

这里我们选取序列中**最右侧**的元素作为基数，并按照从左向右的顺序依次将序列中的元素和基数进行比较，同时记录序列中的当前分割位置（*对应动画中的箭头 P*）。如果当前元素小于基数，则将当前元素和分割位置处的元素进行交换，并将分割位置右移一位。**最后，不要忘了将当前分割位置处的元素和基数进行交换！**这样我们就可以保证分割位置左侧的所有元素值都小于基数，而分割位置及其右侧的所有元素值都大于或等于基数。

![QuickSort_partition.svg](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/QuickSort_partition.svg)

### 快排算法完整实现

实现了子序列的分割，就算是完成了快排算法的核心逻辑，剩下只需要递归的调用自己对分割后的子序列进行快速排序，直到子序列中只剩下一个元素（基本情况）。

下面的代码是带动画可视化的 Python 版本实现：

```python
import algviz

class QuickSort():
    def __init__(self, nums_):
        self.viz = algviz.Visualizer(1.0)
        self.nums = self.viz.createVector(nums_, name='Numbers', cell_size=(40,200), histogram=True)
        self.tree = algviz.RecursiveTree(self.viz)
        self.p = self.viz.createCursor(name='P'); self.nums[self.p]
        self.solve(0, len(nums_)); self.viz.display(3.0)
    
    def solve(self, l, r):
        if l >= r - 1:
            return  # 基本情况：序列中只有一个元素。
        self.tree.forward('{}:{}'.format(l, r-1))
        self.nums.mark(algviz.color_gray, 0, l, hold=True)
        if r < len(self.nums):
            self.nums.mark(algviz.color_gray, r, len(self.nums), hold=True)
        i = l; self.p << l; self.viz.display()
        # 子序列分割代码开始。
        while i < r - 1:
            if self.nums[i] < self.nums[r-1]:
                self.nums.mark(algviz.color_orange, r-1); self.nums.mark(algviz.color_tomato, i); self.viz.display(1.0)
                self.nums.swap(i, self.p); self.viz.display(2.0)
                self.nums.mark(algviz.color_silver, self.p, hold=True); self.p += 1
            else:
                self.nums.mark(algviz.color_orange, r-1); self.nums.mark(algviz.color_lime, i); self.viz.display()
                self.nums.mark(algviz.color_silver, i, hold=True)
            i += 1; self.viz.display(1.0)
        self.nums.swap(self.p, r-1); self.viz.display(2.0)
        # 子序列分割代码结束。
        self.nums.removeMark(algviz.color_gray); self.nums.removeMark(algviz.color_silver)
        self.solve(l, self.p.index())
        self.solve(self.p + 1, r)
        self.tree.backward()

solver = QuickSort([3, -4, -1, 4, -6, -3, 2])
```

*您可以在本地安装 algviz 后直接运行该代码片段！环境配置请参考：[安装步骤]({{ site.url }}/cn/about.html#%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)*

## 动画演示

动画中包括两个数据结构：[递归树]({{ site.url }}/cn/RecursiveTree/)（Recursive tree）和排序数组（Numbers）。

+ 递归树显示算法当前的递归状态：
    + 新产生的子问题使用<font color="#ADFF2F">黄绿色</font>标记；
    + 已解决的子问题使用<font color="silver">银灰色</font>标记；
    + 而当前正在处理的子问题使用<font color="tomato">番茄红色</font>标记。
+ 排序数组是输入的排序序列：
    + 基数元素使用<font color="orange">橙色</font>标记；
    + 当前比基数小的元素使用<font color="lime">亮绿色</font>标记；
    + 当前比基数大的元素使用<font color="tomato">番茄红色</font>标记；
    + 当前正在处理的数组区间以外的元素使用<font color="gray">深灰色</font>淡化；
    + 当前数组的划分位置使用光标 P 来表示。

![QuickSort.svg](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/QuickSort.svg)

## 算法特点

快排算法在一般情况下的时间效率是很高的，而且快排算法可以直接在原始输入序列上进行操作，对储存空间的需求也比归并排序少很多，因此对大规模序列进行排序时有很大优势。但由于**快排算法是不稳定的**（即：不能保证大小相等的两个元素的相对位置和输入序列中的一样），所以在对稳定性有要求的场景中不能使用该算法。

### 时间复杂度

使用递归树来分析快排算法的时间复杂度：在递归树的每一层中，分割子序列所需要的操作加起来为 $O(n)$ ，但由于**子序列的划分不一定是左右平衡的，这与基数的选择有关**，所以递归树的深度是不确定的。如果我们足够幸运，在每次的划分时左右两个子序列的长度都刚好是相等的，那么递归树的深度就是 $O(log_2^n)$，但如果我们非常倒霉，每次划分时其中一个子序列的长度都为 1，那么递归树的深度就是 $O(n)$。

因此，快排算法的时间复杂度在 $O(n \cdot log_2^n)$ ~ $O(n^2)$ 之间。幸运的是，实际情况中的序列往往是趋于离散且均匀分布的，如果我们**随机的选择基数进行划分**，那么递归树大概率是平衡的，所以在实际应用中快排算法的时间复杂度接近于 $O(n \cdot log_2^n)$。

### 空间复杂度

子序列的划分过程可以在输入序列上直接完成，不需要申请额外的储存空间，因此快速排序算法的空间复杂度只与递归树的深度有关。在时间复杂度的分析中，我们知道递归树的深度在 $O(log_2^n)$ ~ $O(n)$ 之间，因此快排算法的空间复杂度也是在 $O(log_2^n)$ ~ $O(n)$ 之间。
