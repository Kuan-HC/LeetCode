# 面試金典 1009 排序矩陣查找
 
給定M×N矩陣，每一行、每一列都按升序排列，請編寫代碼找出某元素。

## Sorted Matrix Search

Given an M x N matrix in which each row and each column is sorted in ascending order, write a method to find an element.

[LeetCode](https://leetcode-cn.com/problems/sorted-matrix-search-lcci/)

### Example 1
```
 [
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

```

### C++ 

```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int rowNum = matrix.size();
        if (rowNum == 0)
            return false;
        int colNum = matrix[0].size();

        int row = rowNum - 1;
        int col = 0;

        while(row >= 0 && col < colNum)
        {
            if(matrix[row][col] > target)
                row -= 1;
            else if(matrix[row][col] < target)
                col += 1;
            else
                return true;
        }

        return false;
    }
};
```
