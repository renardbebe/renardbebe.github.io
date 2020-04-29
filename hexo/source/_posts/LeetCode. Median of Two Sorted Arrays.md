---
title: 4. Median of Two Sorted Arrays
categories: 
- LeetCode
tags:
- Coding
---

### Question：

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume **nums1** and **nums2** cannot be both empty.

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```



### Solution：

问题可以转换为 在两个数组中，找到两个分隔位置 i 和 j，将数组分割成两个部分：

​				          left_part            |         right_part    

​				A[0], A[1], ..., A[i-1]    |   A[i], A[i+1], ..., A[m-1]

​				B[0], B[1], ..., B[j-1]    |   B[j], B[j+1], ..., B[n-1]

使满足：

> 1. len(left_part) = len(right_part)    →    i + j = m - i + n - j
>
>    * i := 0~m
>    * j := (m+n+1)/2 - i
>
> 2. 左边的元素都比右边的小：
>
>    * A[i-1] ≤ A[i]（已满足），A[i-1] ≤ B[j]
>
>    * B[j-1] ≤ B[j]（已满足），B[j-1] ≤ A[i]

**对于分隔位置的选取：**

1. 对于包含 N 个元素的数组，有 N 个可能的分隔位置。
2. 使用二分查找，保证时间复杂度为 O(log (m+n))。

<!--more-->

#### Ⅱ 关键代码

**C++**

```c++
        if (len1 > len2) {
            swap(nums1, nums2);
            swap(len1, len2);
        }
        // len(nums1) < len(nums2)
        int low = 0, high = len1;
        while (low <= high) {
            int mid1 = (low + high) / 2;  // location of partition 1
            // left part >= right part
            int mid2 = ((len1 + len2 + 1) / 2) - mid1;  // location of partition 2
            
            if (mid1 < high && nums1[mid1] < nums2[mid2-1]) {
                // mid1 is too small
                low = mid1 + 1;
            }
            else if (mid1 > low && nums1[mid1-1] > nums2[mid2]) {
                // mid1 is too large
                high = mid1 - 1;
            }
            else {
                int maxLeft = 0, minRight = 0;
                
                // get the max of left partitions
                if (mid1 == 0) maxLeft = nums2[mid2-1];
                else if (mid2 == 0) maxLeft = nums1[mid1-1];
                else maxLeft = max(nums1[mid1-1], nums2[mid2-1]);
                
                // when total length is odd
                if ((len1 + len2) % 2) return maxLeft;
                
                // get the min of right partitions
                if (mid1 == len1) minRight = nums2[mid2];
                else if (mid2 == len2) minRight = nums1[mid1];
                else minRight = min(nums1[mid1], nums2[mid2]);
                
                return (maxLeft + minRight) / 2.0;
            }
        }
```



* 注意数组可能为空
* 注意两个数组长度关系
* 注意奇偶数的情况