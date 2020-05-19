---
title: 二维 vector 初始化
categories: 
- Tips
tags:
- Coding
---



```c++

    // 初始化一个 二维 vector
    vector< vector<int> > vt;
    // 使用另一个 二维 vector 初始化当前二维vector
    vector<vector<int> > vect(vt);
    // 初始化一个 二维 vector 行row, 列column, 且值为 0
    vector<vector<int> > vec(row, vector<int>(column));
    // 初始化一个 二维 vector 行row, 列column, 且值为 data=6 自定义 data
    vector<vector<int> > visited(row, vector<int>(column,6));
    // 初始化一个 二维 vector 行row, 第二个参数为一维 vector;
    vector<vector<int> > vecto(row, vector<int>(vt[0].begin()+1,vt[0].begin()+3));
```

