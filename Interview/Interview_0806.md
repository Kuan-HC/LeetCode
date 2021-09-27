# 面試金典 0806 漢諾塔
 
在經典漢諾塔問題中，有 3 根柱子及 N 個不同大小的穿孔圓盤，盤子可以滑入任意一根柱子。一開始，所有盤子自上而下按升序依次套在第一根柱子上(即每一個盤子只能放在更大的盤子上面)。
移動圓盤時受到以下限制:
(1) 每次只能移動一個盤子;
(2) 盤子只能從柱子頂端滑出移到下一根柱子;
(3) 盤子只能疊在比它大的盤子上。

請編寫程序，用棧將所有盤子從第一根柱子移到最後一根柱子。

你需要原地修改棧。


## Hanota

In the classic problem of the Towers of Hanoi, you have 3 towers and N disks of different sizes which can slide onto any tower. 
The puzzle starts with disks sorted in ascending order of size from top to bottom (i.e., each disk sits on top of an even larger one). 
You have the following constraints:

(1) Only one disk can be moved at a time.
(2) A disk is slid off the top of one tower onto another tower.
(3) A disk cannot be placed on top of a smaller disk.

Write a program to move the disks from the first tower to the last using stacks.


[LeetCode](https://leetcode-cn.com/problems/hanota-lcci/)

### Example 1
```
 Input: A = [2, 1, 0], B = [], C = []
 Output: C = [2, 1, 0]
```

### C++ 

```
class Solution
{
private:
    void recursion(int len, vector<int> &A, vector<int> &B, vector<int> &C)
    {
        if (len == 1)
        {
            C.push_back(A.back());
            A.pop_back();
            return;
        }

        // 將 A 上方的 n-1 個 經由 C 搬到 B
        recursion(len - 1, A, C, B);
        // 將 A 最下面的 的 1 個 經由 C
        C.push_back(A.back());
        A.pop_back();
        // 將 之前搬到Bd  n-1 個 經由 A 搬到 C
        recursion(len - 1, B, A, C);
    }

public:
    void hanota(vector<int> &A, vector<int> &B, vector<int> &C)
    {
        int len = A.size();

        recursion(len, A, B, C);
    }
};

int main(void)
{
    /* input*/
    vector<int> A = {0, 1};
    vector<int> B;
    vector<int> C;

    Solution test;
    test.hanota(A, B, C);

    return 0;
}
```
