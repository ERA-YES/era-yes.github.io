---
layout: blog
title: RMQ问题与ST算法
date: 2023-07-13 20:02:47 
updated: 2023-12-08 12:58:33
tags: 
    - Cpp
    - 算法
categories: Cpp
cover: https://pic.imgdb.cn/item/64bf58991ddac507cc907f2b.webp
---
 # RMQ问题与ST算法
 RMQ(Range Minimum Query)问题是计算机科学中的一个经典问题，涉及到在给定数组的某个范围内查找最小值。ST(Segment Tree)算法是一种著名且高效的数据结构，可用于解决RMQ问题。
 本文将介绍RMQ问题，描述ST算法，并在C++中实现它。
 ## RMQ问题
 给定一个大小为n的数组A以及两个整数i和j，使得1≤i≤j≤n，则RMQ问题是在子数组A[i，j]中查找最小元素。
 暴力解决这个问题的方法是扫描给定范围内的所有元素以查找最小值。然而，这种方法需要O(n)时间复杂度。为了获得更好的时间复杂度，我们可以使用ST算法。
 ## ST算法
 ST算法是一种分治方法，它递归地将数组分成较小的段，并构建树来表示每个段的最小值。树的根节点表示整个数组的最小值，而每个叶节点表示单个元素。 ST算法的时间复杂度为O(n log n)。
 ### 预处理
 首先，我们需要进行预处理。假设我们有一个大小为n的数组A，我们要构建ST树，使得每个节点表示从左到右的某个子段的最小值。以下是构建ST树的步骤：
 1. 创建一个数组tree，使它的大小为4*n。这个数组表示了ST树。
 2. 定义一个build函数，它采用递归方法构建ST树。它接受4个参数：tree的节点编号，该节点表示的子段的左右端点start和end，以及原始数组A。如果该节点表示单个元素，则该节点的值等于A[start]。否则，我们递归地构建左右子节点，然后将该节点的值设置为左右子节点的最小值。
 3. 在build函数中调用build(1,0,n-1)。这将构建ST树的整个结构。 这是一个示例代码：
```cpp
const int MAXN = 1e5 + 1; //数组的最大长度
 int a[MAXN]; //存储数组元素的数组
 int tree[MAXN * 4]; //存储ST树的数组
 void build(int node, int start, int end) {
     if (start == end) {
         tree[node] = a[start];
     } else {
         int mid = (start + end) / 2;
         build(2 * node, start, mid);
         build(2 * node + 1, mid + 1, end);
         tree[node] = min(tree[2 * node], tree[2 * node + 1]);
     }
 }
 int main() {
     int n;
     cin >> n;
     for (int i = 0; i < n; i++) {
         cin >> a[i];
     }
     build(1, 0, n - 1);
     return 0;
 }
```
### 询问
 然后，我们可以查询ST树中的最小值。以下是查询的步骤：
 1. 创建一个query函数，它采用递归方法查询最小值。它接受5个参数：tree的节点编号，该节点表示的子段的左右端点start和end，以及查询的区间[l，r]，其中[l，r]表示我们要查找最小值的子段。如果该节点的子段完全在[l，r]之外，则返回一个极大值。如果该节点的子段完全包含在[l，r]之内，则返回该节点的值。否则，我们递归地查询左右子节点，并返回左右子节点的最小值。
 2. 在循环中，调用query(1,0,n-1,l-1,r-1)，其中l和r是我们要查询的区间。我们将l和r减1，因为数组是从0开始索引的，而不是从1开始索引的。 这是一个示例代码：
```cpp
int query(int node, int start, int end, int l, int r) {
     if (r < start || end < l) {
         return INT_MAX; //极大值
     }
     if (l <= start && end <= r) {
         return tree[node];
     }
     int mid = (start + end) / 2;
     int p1 = query(2 * node, start, mid, l, r);
     int p2 = query(2 * node + 1, mid + 1, end, l, r);
     return min(p1, p2);
 }
 int main() {
     int n, q;
     cin >> n >> q;
     for (int i = 0; i < n; i++) {
         cin >> a[i];
     }
     build(1, 0, n - 1);
     while (q--) {
         int l, r;
         cin >> l >> r;
         cout << query(1, 0, n - 1, l - 1, r - 1) << "\n";
     }
     return 0;
 }
```
