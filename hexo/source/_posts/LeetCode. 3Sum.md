---
title: 15. 3Sum
categories: 
- LeetCode
tags:
- Coding
---

### Question：

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



### Solution：

1. 对数组进行排序
2. 遍历首位，将问题转化为 sum = target - nums[i] 的 2Sum
3. 使用两个指针对 2Sum 求解
   * p1 := i+1 ~ p2（有序，前面的已经计算过一遍了）
   * p2 := p1 ~ nums.size()-1
4. 去重（3 个数的和一定，当其中的 2 个数一样时，第 3 个数一定一样）



<!--more-->

#### Ⅱ 关键代码

**C++**

```c++
        // sort the array
		sort(num.begin(), num.end());

        // outer loop
		for (int i = 0; i < num.size(); i++) {
            int target = 0 - num[i];
            int front = i + 1;
            int back = num.size() - 1;

            // two pointors
            while (front < back) {
                int sum = num[front] + num[back];
                if (sum < target) 
                    front++;
                else if (sum > target) 
                    back--;
                else {
                    vector<int> triplet(3, 0);
                    triplet[0] = num[i];
                    triplet[1] = num[front];
                    triplet[2] = num[back];
                    res.push_back(triplet);

                    // Processing duplicates of Number 2
                    // Rolling the front pointer to the next different number forwards
                    while (front < back && num[front] == triplet[1]) front++;

                    // Processing duplicates of Number 3
                    // Rolling the back pointer to the next different number backwards
                    while (front < back && num[back] == triplet[2]) back--;
                }
            }

            // Processing duplicates of Number 1
            while (i + 1 < num.size() && num[i + 1] == num[i]) i++;
        }
```

