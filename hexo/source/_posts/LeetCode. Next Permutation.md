---
title: 31. Next Permutation
categories: 
- LeetCode
tags:
- Coding
---

### Question：

找到自然顺序下的下一个全排列.

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **[in-place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

`1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1`



### Solution：

根据全排列的规律。

1. 从前往后找到第一个降序位置：4
   12431
        ^
2. 对从该位置到结尾的降序序列进行翻转：
   12134
        ^^^
3. 找到降序位置的前一个数字：2
   12134
     ^
4. 从前往后找到降序序列中第一个比它大的数字：3
   12134
          ^
5. 交换：13124

<!--more-->

#### Ⅱ 关键代码

**C++**

```c++
        int len = nums.size();
        int startPos = len-1, endPos = len-1, firstPos = 0;
        for (int i = endPos-1; i >= 0; i--) {
            if (nums[i+1] <= nums[i]) {
                startPos = i;
            }
            else break;
        }
        
        // reverse decreasing part
        int j = endPos;
        for (int i = startPos; i <= j; i++) {
            swap(nums[i], nums[j]);
            j--;
        }
        
        if(startPos > 0) {
            int desNum = nums[startPos-1];
            for (int i = startPos; i <= endPos; i++) {
                if (desNum < nums[i]) {
                    firstPos = i;
                    break;
                }
            }
            swap(nums[startPos-1], nums[firstPos]);
        }
```

