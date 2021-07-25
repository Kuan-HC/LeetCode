# 劍指 Offer 33 二叉搜索樹的後序遍歷序列

輸入一個整數數組，判斷該數組是不是某二叉搜索樹的後序遍歷結果。如果是則返回 true，否則返回 false。假設輸入的數組的任意兩個數字都互不相同。

[LeetCode](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

參考以下這顆二叉搜索樹：
```

     5
    / \
   2   6
  / \
 1   3
```

### Example 1

```
輸入: [1,6,3,2,5]
輸出: false
```

### Example 2

```
輸入: [1,3,2,6,5]
輸出: true
 ```

* 數組長度 <= 1000




## Solution  

### C++

* 時間複雜度：O(n)

* 空間複雜度：O(1)

```
#include <vector>

using namespace std;

class Solution
{
public:
    int majorityElement(vector<int> &nums)
    {
        int key = nums[0];
        int count = 0;

        for (const int &num : nums)
        {
            if (key == num)
                count++;
            else
                count--;

            if (count == 0)
            {
                key = num;
                count = 1;
            }
        }

        return key;
    }
};

int main()
{
    /* input*/
    vector<int> input = {1, 2, 3, 2, 2, 2, 5, 4, 2};

    /* Test*/
    Solution test;
    int res = test.majorityElement(input);

    return 0;
}
```