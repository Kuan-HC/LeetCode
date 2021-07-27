# 劍指 Offer 45 把數組排成最小的數

輸入一個非負整數數組，把數組里所有數字拼接起來排成一個數，打印能拼接出的所有數字中最小的一個。

[LeetCode](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

### Example 1

```
輸入: [10,2]
輸出: "102"
```

### Example 1

```
輸入: [3,30,34,5,9]
輸出: "3033459"
```

* 0 < nums.length <= 100

## Solution  

### C++

* 時間複雜度：O(NlogN) ： N 為最終返回值的字符數量；使用快排或內置函數的平均時間覆雜度為 O(NlogN) ，最差為 O(N^2)

* 空間複雜度：O(N) ： 字符串列表 numStrings 占用線性大小的額外空間。

* 將相鄰string相加後做比較 

```
#include <vector>
#include <string>
#include <algorithm>

using namespace std;


class Solution
{
private:
    static bool comp(const string &lhs, const string &rhs)
    {
        return (lhs + rhs) < (rhs + lhs);
    }

public:
    string minNumber(vector<int> &nums)
    {
        string ret;
        int len = nums.size();
        if(len == 0)
            return ret;
        
        vector<string> numStrings(len);

        for(int i = 0; i <len; ++i)
            numStrings[i] = to_string(nums[i]);

        sort(numStrings.begin(), numStrings.end(), comp);

        for(const auto& str: numStrings)
            ret += str;

        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> input = {3,30,34,5,9};

    /* Test*/
    Solution test;
    string res = test.minNumber(input);

    
    return 0;
}
```