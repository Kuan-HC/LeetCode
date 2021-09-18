# 面試金典 1003 稀疏數組搜索

有個排好序的字符串數組，其中散布著一些空字符串，編寫一種方法，找出給定字符串的位置。
 
##  Sparse Array Search

Given a sorted array of strings that is interspersed with empty strings, write a method to find the location of a given string.

[LeetCode](https://leetcode-cn.com/problems/sparse-array-search-lcci/)


### Example 1

```
Input: words = ["at", "", "", "", "ball", "", "", "car", "", "","dad", "", ""], s = "ta"
 Output: -1
 Explanation: Return -1 if s is not in words.
```

### Example 2

```
Input: words = ["at", "", "", "", "ball", "", "", "car", "", "","dad", "", ""], s = "ball"
 Output: 4

```

### C++ 

* 時間複雜度 O(log n)

* 空間複雜度 O(1)

```
class Solution {
public:
    int findString(vector<string>& words, string s)
    {
        int left = 0;
        int right = words.size() - 1;

        int mid = 0;

        while(left <= right)
        {
            mid = left + (right - left)/2;
            while(words[mid] == "" && mid > left )
                mid--;
            
            if(words[mid] == s)
                return mid;
            else if(words[mid] > s)
                right = mid - 1;
            else    
                left = mid + 1;
        }

        return -1;
    }
};
```
