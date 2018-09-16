---
title: leetcode-4.Median of Two Sorted Arrays
date: 2018-08-10 16:47:15
tags:
- python
- 算法
categories:
- leetcode
---

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume **nums1** and **nums2** cannot be both empty.

<!-- more -->

 ### 思路

题目是让我们求两个数组的中位数，如果没有时间复杂度限制条件的话，最简单好理解的方法是：把两个数组merge成一个sorted array，然后判断数组的长度的奇偶后直接可以得出中位数。

不过题目设置了时间复杂度O(log(m+n))，m和n分别是两个数组的长度。因此题目变得复杂了，这边我主要介绍一种我认为相对好理解的解法。

**该方法的核心是将原问题转变成一个寻找第k小数的问题（假设两个原序列升序排列），这样中位数实际上是第(m+n)/2小的数。所以只要解决了第k小数的问题，原问题也得以解决。**

首先假设数组A和B的元素个数都大于k/2，我们比较A[k/2-1]和B[k/2-1]两个元素，这两个元素分别表示A的第k/2小的元素和B的第k/2小的元素。这两个元素比较共有三种情况：>、<和=。

如果A[k/2-1]<B[k/2-1]，这表示A[0]到A[k/2-1]的元素都在A和B合并之后的前k小的元素中。换句话说，A[k/2-1]不可能大于两数组合并之后的第k小值，所以我们可以将其抛弃。

当A[k/2-1]>B[k/2-1]时存在类似的结论。

当A[k/2-1]=B[k/2-1]时，我们已经找到了第k小的数，也即这个相等的元素，我们将其记为m。由于在A和B中分别有k/2-1个元素小于m，所以m即是第k小的数。(这里可能有人会有疑问，如果k为奇数，则m不是中位数。这里是进行了理想化考虑，在实际代码中略有不同，是先求k/2，然后利用k-k/2获得另一个数。)

通过上面的分析，我们即可以采用递归的方式实现寻找第k小的数。此外我们还需要考虑几个边界条件：

- 如果A或者B为空，则直接返回B[k-1]或者A[k-1]；
- 如果k为1，我们只需要返回A[0]和B[0]中的较小值；
- 如果A[k/2-1]=B[k/2-1]，返回其中一个；

### 代码

```python
def findKth(nums1, m, nums2, n, k):
    if m>n:
        return findKth(nums2, n, nums1, m, k)
    if m==0:
        return nums2[k-1]
    if k==1:
        return min(nums1[0], nums2[0])
    pa = min(k//2, m)
    pb = k - pa
    if nums1[pa-1]<nums2[pb-1]:
        return findKth(nums1[pa:], m-pa, nums2, n, k-pa)
    elif nums1[pa-1]>nums2[pb-1]:
        return findKth(nums1, m, nums2[pb:], n-pb, k-pb)
    else:
        return nums1[pa-1]
    
class Solution:
    def findMedianSortedArrays(nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        m = len(nums1)
        n = len(nums2)
        k = (m+n)//2
        if (m+n)%2 == 0:
            return (findKth(nums1, m, nums2, n, k)+findKth(nums1, m, nums2, n, k+1))/2
        else:
            return findKth(nums1, m, nums2, n, k+1)
```

参考资料：[leetcode之 median of two sorted arrays - CSDN博客](https://blog.csdn.net/yutianzuijin/article/details/11499917)

