# 面試金典 1011 峰與谷
 
在一個整數數組中，“峰”是大於或等於相鄰整數的元素，相應地，“谷”是小於或等於相鄰整數的元素。
例如，在數組{5, 8, 4, 2, 3, 4, 6}中，{8, 6}是峰， {5, 2}是谷。現在給定一個整數數組，將該數組按峰與谷的交替順序排序。

## Peaks and Valleys

In an array of integers, a "peak" is an element which is greater than or equal to the adjacent integers and a "valley" is an element which is less than or equal to the adjacent inte­gers. For example, in the array {5, 8, 4, 2, 3, 4, 6}, {8, 6} are peaks and {5, 2} are valleys. Given an array of integers, sort the array into an alternating sequence of peaks and valleys.


[LeetCode](https://leetcode-cn.com/problems/sorted-merge-lcci/)

### Example 1
```
Input: [5, 3, 1, 2, 3]
Output: [5, 1, 3, 2, 3]
```

### C++ 

```
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        
        vector<int> copy = nums;
        sort(copy.begin(), copy.end());

        int left = 0;
        int right = nums.size()-1;
        int ptr = 0;

        bool odd = true;

        while( ptr < nums.size())
        {
            if(odd == true)
                nums[ptr++] = copy[left++];
            else
                nums[ptr++] = copy[right--];
            
            odd = odd == true? false: true;
        }
    }
};
```
