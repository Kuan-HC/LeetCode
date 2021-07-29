# 劍指 Offer 57-2 和為s的連續正數序列

輸入一個正整數 target ，輸出所有和為 target 的連續正整數序列（至少含有兩個數）。

序列內的數字由小到大排列，不同序列按照首個數字從小到大排列。

 
[LeetCode](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)


### Example 1

```
輸入：target = 9
輸出：[[2,3,4],[4,5]]
示例 2：
```

### Example 2

```
輸入：target = 15
輸出：[[1,2,3,4,5],[4,5,6],[7,8]]

```

* 1 <= target <= 10^5


## Solution  

### C++

* 時間複雜度：由於兩個指針移動均單調不減，且最多移動 target/2 次，即方法一提到的枚舉的上界，所以時間覆雜度為 O(target) 。

* 空間複雜度：O(1) 除了答案數組只需要常數的空間存放若幹變量

```
#include <vector>

using namespace std;

class Solution
{
private:
    vector<vector<int>> ret;
    vector<int> tmp;
    inline int sum(int &left, int &right)
    {
        return (left + right) * (right - left + 1) / 2;
    }

    inline void storeVector(int &left, int &right)
    {
        tmp.clear();
        for(int i = left; i<= right; ++i)
            tmp.push_back(i);
        ret.emplace_back(tmp);
    }

public:
    vector<vector<int>> findContinuousSequence(int target)
    {
        /* result contents at least two digits*/
        int left = 1;
        int right = 2;

        int tmptSum = 0;
        /* use equation to find upper limit*/
        while (left < right)
        {
            tmptSum = sum(left, right);
            if (tmptSum < target)
                ++right;
            else if (tmptSum > target)
                ++left;
            else
            {
                /* store record into result*/
                storeVector(left, right);
                /* next sequential*/
                ++left;
                ++right;
            }
        }

        return ret;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    vector<vector<int>> res = test.findContinuousSequence(1);

    return 0;
}

```