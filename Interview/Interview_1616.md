# 面試金典 1616 部份排序

給定一個整數數組，編寫一個函數，找出索引m和n，只要將索引區間[m,n]的元素排好序，整個數組就是有序的。
注意：n-m盡量最小，也就是說，找出符合條件的最短序列。函數返回值為[m,n]，若不存在這樣的m和n（例如整個數組是有序的），請返回[-1,-1]。

## 
Given an array of integers, write a method to find indices m and n such that if you sorted elements m through n,
the entire array would be sorted. Minimize n - m (that is, find the smallest such sequence).

Return [m,n]. If there are no such m and n (e.g. the array is already sorted), return [-1, -1].

 
[LeetCode](https://leetcode-cn.com/problems/sub-sort-lcci/)

### Example 1
```
Input:  [1,2,4,7,10,11,7,12,6,7,16,18,19]
Output:  [3,9]
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(1)

```
class Solution
{
public:
    vector<int> subSort(vector<int> &array)
    {
        int len = array.size();

        int maxTemp = INT_MIN;
        int minVal = INT_MAX;
        int valueLowerMax = -1;

        int i = 0;
        for (; i < len; ++i)
        {
            if (array[i] >= maxTemp)
            {
                maxTemp = array[i];
                continue;
            }
            valueLowerMax = i;
            minVal = min(minVal, array[i]);
        }

        if (valueLowerMax == -1)
            return vector<int>{-1, -1};

        for (i = 0; i < len; ++i)
        {
            if (minVal < array[i])
                break;
        }

        return vector<int>{i , valueLowerMax};
    }
};

int main(void)
{
    /* input*/
    vector<int> input = {1, 2, 4, 7, 10, 11, 7, 12, 6, 7, 16, 18, 19};

    /* test*/
    Solution test;
    vector<int> res = test.subSort(input);

    return 0;
}
```
