---
layout: post
title:  "Bubble sort algorithm"
date:   2022-09-22 20:09:00 +0800
categories: SortingAlgorithm
topmost: false
latex: false
lang: en
sec_svg: true
excerpt: Bubble sort is a sorting algorithm that we are familiar with. It is named after the algorithm that runs like bubbles emerging from the water.
---


Bubble sort is a sorting algorithm that we are familiar with. It is named after the algorithm that runs like bubbles emerging from the water.

Just like the animation below: as the algorithm runs, the bigger elements in the sequence gradually move from the left to the right:

![bubble_sort_example](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/BubbleSort.svg)

## Fundamental

The bubble sort algorithm is similar to the [insertion sort algorithm]({{ site.url }}/en/InsertionSort/). The algorithm compares the size of two adjacent elements in turn during each round of scanning and if the two elements are in reverse order, the algorithm swaps the positions of the two elements. Suppose the algorithm scans from left to right, and each time it puts the larger of the two adjacent elements in the right. Then after this round of scanning, the maximum value in the scanned sequence will run to the far right of the scanned sequence. The bubble sort algorithm repeats the scanning process until all the elements are sorted.

The bubble sort algorithm is also a **comparison-based** sorting algorithm and the sorting results are stable. The bubble sort algorithm needs *O(n^2)* comparison operations regardless of the sequence of the input data. Therefore, in some cases, the algorithm is not as efficient as the insertion sort algorithm. And for large-scale cases, the bubble sort algorithm also dones't have any advantage except for its simplicity.

## Implementation

This is the Python implementation of bubble sort algorithm:

```python
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

*You can run this code snippet directly after installing algviz locally! For environment configuration, please refer to the [Installation]({{ site.url }}/en/about.html#installation) page.*

## Reference

+ [VisuAlgo algorithm visualization](https://visualgo.net/en)
