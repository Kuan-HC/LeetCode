# 面試金典 1604 最小差

給定兩個整數數組a和b，計算具有最小差絕對值的一對數值（每個數組中取一個值），並返回該對數值的差

## Smallest Difference 
Given two arrays of integers, compute the pair of values (one value in each array) with the smallest (non-negative) difference.
Return the difference.
 
[LeetCode](https://leetcode-cn.com/problems/smallest-difference-lcci/)

### Example 1

```
Input: {1, 3, 15, 11, 2}, {23, 127, 235, 19, 8}
Output:  3, the pair (11, 8)
```

* 1 <= a.length, b.length <= 100000
* -2147483648 <= a[i], b[i] <= 2147483647
* 正確結果在區間 [0, 2147483647] 內


### C++ 

* 時間複雜度 O(n)

* 空間複雜度 O(1)

```
class Solution {
public:
    int smallestDifference(vector<int>& a, vector<int>& b) {
        sort(a.begin(), a.end());
        sort(b.begin(), b.end());

        int len1 = a.size();
        int len2 = b.size();

        int ptr1 = 0;
        int ptr2 = 0;

        long  diff = 0;
        long ret = LONG_MAX;

        while( ptr1 < len1 && ptr2 < len2)
        {
            diff = abs(a[ptr1] - b[ptr2]);            
            if (diff == 0)
                return 0;

            ret = min(ret, diff);

            a[ptr1] > b[ptr2]? ptr2++:ptr1++; 
        }

        return (int)ret;      
    }
};
```
