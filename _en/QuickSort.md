---
layout: post
title:  "Quick Sort Algorithm"
date:   2022-10-13 21:46:00 +0800
categories: SortingAlgorithm Recursive
topmost: false
latex: true
lang: en
sec_svg: true
excerpt: The Quicksort algorithm was first proposed by Charles Antony Richard Hoare, also called the partition-exchange sort algorithm. The Quicksort algorithm has high execution efficiency in general and is widely used in practical engineering.
---

The Quicksort algorithm was first proposed by Charles Antony Richard Hoare, also called the **partition-exchange sort algorithm**. The Quicksort algorithm has high execution efficiency in general and is widely used in practical engineering.

## Fundamental

The Quicksort algorithm uses the idea of **divide and conquer**, which is similar to the [Mergesort algorithm]({{ site.url }}/en/MergeSort/). But the Quicksort algorithm uses a very clever way to divide the subsequences, Instead of simply splitting the sequence in half from the middle like the merge sort algorithm.

**The Quicksort algorithm divides the sequence into left and right segments, and ensures that the largest element in the left sequence is smaller than the smallest element in the right sequence.** To implement this, The Quicksort algorithm picks an element from the current sequence as the **radix**, and split the sequence based on the radix. When splitting, the algorithm ensures that the subsequences to the left of the radix are all less than the radix, while the subsequences to the right of the radix are all greater than or equal to the radix.

## Implementation

### Subsequence segmentation

The animation below shows the subsequence segmentation process:

Let's pick the **rightmost element** in the sequence as the radix, and compare the elements in the sequence with the radix in order from left to right. At the same time, we record the current split position in the sequence(*corresponds to the arrow P in the animation*). If the current element is less than the radix, swap the current element with the element at the split position, and shift the split position to the right by one. **Last but not least, don't forget to swap the element at the current split position with the radix!** Then we can guarantee that all element values to the left of the split position are less than the radix, while the split position and all element values to its right are greater than or equal to the radix.

![QuickSort_partition.svg](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/QuickSort_partition.svg)

### Quicksort algorithm implementation

Once the subsequence segmentation is realized, the core logic of the Quicksort algorithm is completed. The algorithm just need to recursively call ourselves to quickly sort the split subsequences, until only one element remains in the subsequence(basic situation).

The following code is the Python version implementation with animated visualization:

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
            return  # Basic situation: just one element left in the subsequence.
        self.tree.forward('{}:{}'.format(l, r-1))
        self.nums.mark(algviz.color_gray, 0, l, hold=True)
        if r < len(self.nums):
            self.nums.mark(algviz.color_gray, r, len(self.nums), hold=True)
        i = l; self.p << l; self.viz.display()
        # Subsequence segmentation beigin.
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
        # Subsequence segmentation end.
        self.nums.removeMark(algviz.color_gray); self.nums.removeMark(algviz.color_silver)
        self.solve(l, self.p.index())
        self.solve(self.p + 1, r)
        self.tree.backward()

solver = QuickSort([3, -4, -1, 4, -6, -3, 2])
```

*You can run this code snippet directly after installing algviz locally! For environment configuration, please refer to the [Installation]({{ site.url }}/en/installation.html) page.*

## Animation Demo

There are two data structures in the animation, which is the [RecursiveTree]({{ site.url }}/en/RecursiveTree/) and Numbers:

+ The recursion tree shows the current recursive state of the algorithm:
    + The new generated subproblem is marked by <font color="#ADFF2F">green yellow</font> color.
    + The solved subproblem is marked by<font color="silver">silver</font> color.
    + The currently solving subproblem is marked by <font color="tomato">tomato</font> color.
+ Numbers is the input sequence to be sorted:
    + The radix is marked by <font color="orange">orange</font> color.
    + The element that smaller than radix is marked by <font color="lime">lime</font> color.
    + The element that bigger than radix is marked by <font color="tomato">tomato</font> color.
    + Elements outside the range of the array currently being processed use the <font color="gray">gray</font> color to mark.
    + The split position of the current array is indicated by the **cursor P**.

![QuickSort.svg](https://cdn.jsdelivr.net/gh/zjl9959/algviz-launch@master/svgs/QuickSort.svg)

## Features

The Quicksort algorithm is very time efficient in general. And the Quicksort algorithm can operate directly on the original input sequence, and it requires less storage space than merge sort, so it has a great advantage when sorting large-scale sequences. But since **the Quicksort algorithm is unstable**(that is: there is no guarantee that the relative positions of two elements of equal size are the same as in the input sequence). Therefore, the QuickSort algorithm cannot be used in scenarios that require stability.

### Time Complexity

Let's use recursion tree to analyze the time complexity of Quicksort algorithm: in each level of the recursion tree, The operations required to split a subsequence add up to $O(n)$. However, since **the division of subsequences is not necessarily balanced left and right, that is related to the choice of radix**, So the depth of the recursion tree is indeterminate. If we are lucky enough: in each division, the lengths of the left and right subsequences are exactly equal, then the depth of the recursion tree is $O(log_2^n)$. But if we are very unlucky, one of the subsequences at each division has the length of 1, then the depth of the recursion tree is $O(n)$.

So, the time complexity of the Quicksort algorihtm is in range $O(n \cdot log_2^n)$ ~ $O(n^2)$. Fortunately, In practice, the sequence tends to be discrete and uniformly distributed. If we **randomly choose the radix** to do the divide work, Then the recursive tree has a high probability of being balanced. Therefore, the time complexity of the Quicksort algorithm in practical applications is close to $O(n \cdot log_2^n)$.

### Space Complexity

The subsequence division process can be done directly on the input sequence without additional storage space, so the space complexity of the Quicksort algorithm is only related to the depth of the recursion tree. In the analysis of time complexity, we know that the depth of the recursion tree is between $O(log_2^n)$ ~ $O(n)$. Therefore, the space complexity of the Quicksort algorithm is in range $O(log_2^n)$ ~ $O(n)$.
