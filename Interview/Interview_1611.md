# 面試金典 1611 跳水板

你正在使用一堆木板建造跳水板。有兩種類型的木板，其中長度較短的木板長度為shorter，長度較長的木板長度為longer。你必須正好使用k塊木板。
編寫一個方法，生成跳水板所有可能的長度。

返回的長度需要從小到大排列。
 
##  Diving Board

You are building a diving board by placing a bunch of planks of wood end-to-end. There are two types of planks, one of length shorter and one of length longer. 
You must use exactly K planks of wood. Write a method to generate all possible lengths for the diving board.

return all lengths in non-decreasing order.


[LeetCode](https://leetcode-cn.com/problems/diving-board-lcci/)

### Example 1
```
Input: 
shorter = 1
longer = 2
k = 3
Output:  {3,4,5,6}
```


### C++ 

* 時間複雜度 O(k) 

* 空間複雜度 O(1)

```
class Solution
{
public:
    vector<int> divingBoard(int shorter, int longer, int k)
    {
        vector<int> ret;
        if (k == 0)
            return vector<int>{};

        if (shorter == longer)
            return vector<int>{longer * k};

        int length = shorter * k;

        for (int i = 0; i <= k; ++i)
            ret.push_back(length - shorter * i + longer * i);

        return ret;
    }
};
```
