---
layout: post
title:  "冒泡排序算法"
date:   2022-09-22 20:09:00 +0800
categories: 排序算法
topmost: false
latex: false
lang: zh
sec_svg: true
excerpt: 冒泡排序是大家接触的比较多的一种排序算法，因算法运行起来像是气泡冒出水面而得名。
---


冒泡排序是大家接触的比较多的一种排序算法，因算法运行起来像是气泡冒出水面而得名。

就像下面的动画：随着算法的运行，序列中较大的元素从序列的左侧逐渐移动到右侧：

![bubble_sort_example](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/BubbleSort.svg)

## 基本原理

冒泡排序和[插入排序](https://algviz.com/cn/InsertionSort/)较为相似，算法在每轮的扫描过程中依次比较两个相邻元素的大小，如果两个元素是逆序的，则交换两元素的位置。假设算法从左向右扫描➡，每次将相邻两个元素中较大的元素放到后面，那么经过该轮扫描之后，扫描过的序列中的最大值将会跑到扫描序列最右边的位置，重复执行扫描过程直到所有元素都被排序即可。

冒泡排序算法同样属于基于比较的排序算法，排序结果具有稳定性，但无论输入数据的序列如何，算法都需要进行 *O(n^2)* 次的比较操作，因此在部分算例上该算法不如插入排序算法高效。对于大规模算例，冒泡排序更是慢的让人头皮发麻。

## 算法实现

下面是冒泡排序算法的 Python 代码实现：

```python
# 冒泡排序实现。
import algviz

def bubble_sort(data):
    viz = algviz.Visualizer(2)
    vector = viz.createVector(data, cell_size=(40, 160), show_index=False, histogram=True)
    i = viz.createCursor(name='i')
    j = viz.createCursor(name='j')
    for e in range(len(vector)):
        i << 0; j << 1
        while j < len(vector) - e:
            viz.display(1.0)
            if vector[i] > vector[j]:
                vector.mark(algviz.color_red, i); vector.mark(algviz.color_green, j); viz.display(1.0)
                vector.swap(i, j); viz.display()
            else:
                vector.mark(algviz.color_red, j); vector.mark(algviz.color_green, i); viz.display(1.0)
            i += 1; j += 1
        vector.mark(algviz.color_gray, len(vector)-e-1, hold=True)
    vector.removeMark(algviz.color_gray); viz.removeCursor(i); viz.removeCursor(j); viz.display()

bubble_sort([5, 3, -2, 3, -1, 1, 4])
```

*您可以在本地安装 algviz 后直接运行该代码片段！环境配置请参考：[安装步骤](https://algviz.com/cn/about.html#%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)*

## 参考链接

+ [十大经典排序算法+动图演示](https://www.cnblogs.com/onepixel/articles/7674659.html)
