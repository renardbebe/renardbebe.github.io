---
title: 33. Search in Rotated Sorted Array
categories: 
- LeetCode
tags:
- Coding
---

### Question：

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```



### Solution：

**The array is sorted, except it might drop at one point.**

* **If nums[0] <= nums[i]**, then nums[0..i] is sorted (in case of "**==**" it's just one element, and in case of "**<**" there must be a drop elsewhere). So we should keep searching in nums[0..i] if the target lies in this sorted range, i.e., if `nums[0] <= target <= nums[i]`.
* **If nums[i] < nums[0]**, then nums[0..i] contains a drop, and thus nums[i+1..end] is sorted and lies strictly between nums[i] and nums[0]. So we should keep searching in nums[0..i] if the target *doesn't* lie strictly between them, i.e., if `target <= nums[i] < nums[0]` or `nums[i] < nums[0] <= target`



<!--more-->

#### Ⅱ 关键代码

**C++**

```c++
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        // check whether exactly two of them are true
        if (nums[mid] == target)
               return mid;
        if (nums[0] <= target < nums[mid] or 
            target < nums[mid] < nums[0] or 
            nums[mid] < nums[0] <= target)
               hi = mid - 1;
        else
            low = mid + 1;
    }
```

