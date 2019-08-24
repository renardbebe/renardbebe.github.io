---
title: 2. Trailing Zeros
categories: 
- LintCode
tags:
- Coding
---

### Question：

给定一个数字 *n*，求 *n!* 的结尾有多少个0。



### Solution：

#### Ⅰ 思路

通过乘法能产生0的，需要2x5，因此只需要统计阶乘中有多少个因子5即可。

<!--more-->

#### Ⅱ 关键代码

```python
        cnt = 0
        while (n) :
            cnt += int(n/5)
            n /= 5
        return cnt
```



### Conclusion：

**\> 如何求 n! 某个因子 a 的个数？**

1. n! 可以拆解为 a 的倍数，和 others
2. 因为 k 是阶乘中最大的 a 的倍数，故 $k = int(n/a)$
3. 从(4)式中可以提取出 k 个 a，然后再用同样的方法分解 k!

$$
\begin{align}
n! &= 1*2*3*…*(n-2)*(n-1)*n \\
&= (a*2a*3a*...*ka)*others \\
&= a^k*(1*2*3*...*k)*others \\
&= a^k*k!*others
\end{align}
$$



