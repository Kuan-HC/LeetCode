# 面試金典 1001 合並排序的數組

給定兩個排序後的數組 A 和 B，其中 A 的末端有足夠的緩沖空間容納 B。 編寫一個方法，將 B 合並入 A 並排序。

初始化 A 和 B 的元素數量分別為 m 和 n。

## Sorted Merge

You are given two sorted arrays, A and B, where A has a large enough buffer at the end to hold B. Write a method to merge B into A in sorted order.

Initially the number of elements in A and B are m and n respectively.


[LeetCode](https://leetcode-cn.com/problems/sorted-merge-lcci/)

### Example 1
```
Input:
A = [1,2,3,0,0,0], m = 3
B = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

### C++ 


```
class Solution
{
public:
    void merge(vector<int> &A, int m, vector<int> &B, int n)
    {
        int ptr1 = m - 1;
        int ptr2 = n - 1;
        int tail = m + n - 1;

        while( ptr1 >= 0 || ptr2 >= 0)
        {
            if( ptr1 == -1)
                A[tail--] = B[ptr2--];
            else if( ptr2 == -1)
                return;
            else if(A[ptr1] < B[ptr2])
                A[tail--] = B[ptr2--];
            else if(A[ptr1] >= B[ptr2])
                A[tail--] = A[ptr1--];
        }
    }
};
```
