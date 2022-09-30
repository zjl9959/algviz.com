---
layout: post
title:  "Insertion sort algorithm"
date:   2022-09-17 22:07:00 +0800
categories: SortingAlgorithm
topmost: false
latex: true
lang: en
sec_svg: true
excerpt: Insertion sort is a simple and naive sorting method, which processes the unsorted elements in the unordered part sequentially and inserts them into the correct position in the sorted part.
---

Insertion sort is a simple and naive sorting method, which processes the unsorted elements in the unordered part sequentially and inserts them into the correct position in the sorted part.

## Fundamental

Suppose we have an unordered set of elements, we can divide it into two parts, one part needs to be arranged in order from small to large, and the other part remains unordered. Then, we just need to take one element from the unordered part at a time and insert it into the correct position in the ordered part.

The process of finding a suitable insertion position can be simplified to find a position $i$ in the ordered part, so that the element at position $i$ is less than or equal to the element to be inserted, and the element at position $i+1$ is greater than the element to be inserted.

## Implementation

Here is the Python code implementation of the insertion sort algorithm (with animation demonstration):

```python
import algviz

def insertSort(nums_):
    viz = algviz.Visualizer(delay=2)
    nums = viz.createVector(data=nums_, cell_size=(40,200), histogram=True, show_index=False)
    # Start with the second element.
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
            # Inserts an element after the first element to its left that is not larger than it.
            nums.insert(i + 1, nums.pop(j))
            nums.removeMark(algviz.color_green); viz.display()
        nums.removeMark(algviz.color_silver)
    viz.display()

insertSort([5, 3, -2, 3, -1, 1, 4])
```

*You can run this code snippet directly after installing algviz locally! For environment configuration, please refer to the [Installation](http://localhost:4000/en/about.html#installation) page.*

### Animation Demo

For the convenience of observation, the array is divided into two parts: an ordered part and an unordered part (marked in gray). The algorithm processes the leftmost element (marked in red) in the unordered part each round, and compare the element with the elements in the ordered part **in order from right to left** 👈. If the element being compared in the ordered part is larger than that element, then it is marked as green, and the algorithm continues to search towards left. Otherwise, it is marked as yellow and the algorithm stops searching and inserts the element to be processed at the current position. As the algorithm runs, we can observe that the unordered part of the array becomes less and less, and we end up with a completely ordered array!

![insertion_sort_example](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/InsertionSort2.svg)

## Features

### Complexity

Two layers of loops are required in the implementation of the insertion sort algorithm. The first level loop processes each unsorted element of the array in turn, and the second level loop finds a suitable insertion position for the element, so the overall **time** complexity is $O(n^2)$.

Insertion sort algorithm can operate directly on the input sequence, and it does not require additional storage space, so the **space** complexity is $O(1)$.

### Scenarios

The insertion sort algorithm belongs to the **comparison-based** sorting algorithm, and the sorting result is stable (that is: *the relative positions of logically equal elements in the original input sequence do not change*).

This algorithm is not suitable for sorting large-scale sequences when the current storage space is relatively cheap and the running speed of the CPU encounters a bottleneck. However, because the algorithm is simple to implement and the constant term in its time complexity is small, the algorithm may run faster on some small-scale problems.

## Optimization

Do we have any optimization opportunities in the link of searching for the right insertion position?

Of course we have! Since the search is performed in an **ordered array**, we can use a faster **binary search** algorithm instead of the original **sequential search** algorithm. Try it yourself if you are interested!

PS: although the time complexity of the binary search algorithm is $O(log_2^n)$, but since the insertion sort algorithm needs $O(n)$ time complexity every time to move the element to be inserted, so the overall time complexity of the algorithm will not be reduced.
