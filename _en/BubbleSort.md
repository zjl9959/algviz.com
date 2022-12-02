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
    viz = algviz.Visualizer(0.5)
    vector = viz.createVector(data, cell_size=(40, 160), histogram=True)
    for i in range(len(vector)):
        for j in range(len(vector)-i-1):
            if vector[j] > vector[j+1]:
                vector.mark(algviz.cRed, j)
                vector.mark(algviz.cGreen, j+1)
                viz.display()
                vector.swap(j, j+1)
            else:
                vector.mark(algviz.cRed, j+1)
                vector.mark(algviz.cGreen, j)
            viz.display()
        vector.mark(algviz.cGray, len(vector)-i-1, hold=True)
    vector.removeMark(algviz.cGray)
    viz.display()

bubble_sort([5, 4, -2, 1, -1, 3])
```

*You can run this code snippet directly after installing algviz locally! For environment configuration, please refer to the [Installation]({{ site.url }}/en/installation.html) page.*

## Reference

+ [VisuAlgo algorithm visualization](https://visualgo.net/en)
