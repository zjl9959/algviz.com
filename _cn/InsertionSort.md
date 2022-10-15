---
layout: post
title:  "插入排序算法"
date:   2022-09-17 22:07:00 +0800
categories: 排序算法
topmost: false
latex: true
lang: zh
sec_svg: true
excerpt: 插入排序是一种较为简单和朴素的排序方法，它依次对序列中未排序的元素进行处理，将其插入到已排序序列中正确的位置。
---


插入排序是一种较为简单和朴素的排序方法，它依次对序列中未排序的元素进行处理，将其插入到已排序序列中正确的位置。

## 基本原理

假设我们有一组无序的元素，我们可以把它分成两个部分，一部分需要按照从小到大的顺序排列，另一部分则保持无序状态。那么，我们只需要每次从无序部分中拿出一个元素，并把它插入到有序部分中合适的位置即可。

而寻找合适插入位置的过程，可以简化为在有序部分中找到一个位置 $i$，使位置 $i$ 处的元素小于等于要插入的元素，并且位置 $i+1$ 处的元素大于要插入的元素即可。

## 算法实现

以下是插入排序算法的 Python 代码实现（支持动画演示）：

```python
import algviz

def insertSort(nums_):
    viz = algviz.Visualizer(delay=2)
    nums = viz.createVector(data=nums_, cell_size=(40,200), histogram=True, show_index=False)
    # 直接从第二个元素开始。
    for ed in range(1, len(nums_)):
        i = ed - 1; j = ed
        nums.mark(algviz.color_silver, ed, len(nums), hold=True); viz.display(1)
        while i >= 0:
            nums.mark(algviz.color_red, j)
            if nums[i] <= nums[j]:
                nums.mark(algviz.color_gold, i); viz.display(1)
                break
            else:
                nums.mark(algviz.color_green, i, hold=True); viz.display(1)
                i -= 1
        if i + 1 != j:
            # 将元素插入到其左边第一个不大于它的元素后面
            nums.insert(i + 1, nums.pop(j))
            nums.removeMark(algviz.color_green); viz.display()
        nums.removeMark(algviz.color_silver)
    viz.display()

insertSort([5, 3, -2, 3, -1, 1, 4])
```

*您可以在本地安装 algviz 后直接运行该代码片段！环境配置请参考：[安装步骤]({{ site.url }}/cn/about.html#%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)*

### 动画演示

让我们看一下动画中的例子！为了方便观察，这里将数组分成两个部分：有序部分和无序部分（使用灰色标记）。算法每轮处理无序部分中最左侧的一个元素（标记为红色），并将该元素和有序部分中的元素按照**从右到左**的顺序依次进行比较。如果有序部分中被比较的元素大于该元素，那么它被标记为绿色，算法继续向左搜索；否则，它被标记为黄色，同时算法停止搜索，并将要处理的元素插入到当前位置。随着算法的运行，我们可以观察到，数组中无序部分越来越少，最终我们得到一个完全有序的数组！

![insertion_sort_example](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/InsertionSort2.svg)

## 算法特点

### 复杂度

在插入排序的实现过程中需要两层循环，第一层循环依次处理数组中每个未排序的元素，第二层为要处理的元素寻找合适的插入位置，因此算法的整体**时间**复杂度为 $O(n^2)$。

插入排序算法可以直接在输入的序列上进行操作，不需要额外的储存空间，因此算法的**空间**复杂度为 $O(1)$。

### 应用场景

插入排序算法属于**基于比较**的排序算法，且排序结果具有稳定性（即：*逻辑上相等的元素在原始输入序列中的相对位置不会改变*）。在目前储存空间较为廉价，而 CPU 的运行速度遇到瓶颈的情况下，该算法不适用于大规模序列的排序，但由于算法实现简单，其时间复杂度中的常数项较小，因此算法在一些小规模问题上可能会运行得更快。

## 算法优化

仔细想一下，在搜索合适插入位置的环节，我们是否有优化机会呢？

当然是有的！由于是在**有序数组**中进行搜索，所以我们可以使用更快的**二分搜索**算法替代原始的**顺序搜索**算法，大家感兴趣的话可以自己尝试一下。

但需要提醒的是，虽然二分查找算法的时间复杂度为 $O(log_2^n)$，但由于插入排序算法每次都需要 $O(n)$ 的时间复杂度来移动要插入的元素，因此算法的整体时间复杂度并不会降低。
