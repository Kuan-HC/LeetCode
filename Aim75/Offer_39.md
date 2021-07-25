# 劍指 Offer 39 數組中出現次數超過一半的數字

數組中有一個數字出現的次數超過數組長度的一半，請找出這個數字。

你可以假設數組是非空的，並且給定的數組總是存在多數元素。

[LeetCode](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

### Example 1

```
輸入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
輸出: 2
```

* 1 <= 數組長度 <= 50000


## Solution  

### C++

* 時間複雜度：O(n)

* 空間複雜度：O(1)

```
#include <vector>
#include <algorithm>

using namespace std;

class Solution
{
private:
    bool checkTree(vector<int> &nums, int root, int end)
    {
        if (end - root + 1 <= 2)
            return true;

        int leftStart = root + 1;

        while (leftStart <= end && nums[leftStart] > nums[root])
            ++leftStart;

        for (int i = leftStart; i <= end; ++i)
        {
            if (nums[i] > nums[root])
                return false;
        }
        bool rightCheck = checkTree(nums, root + 1, leftStart - 1);
        bool leftCheck = checkTree(nums, leftStart, end);

        return rightCheck && leftCheck;
    }

public:
    bool verifyPostorder(vector<int> &postorder)
    {
        int len = postorder.size();
        if (len <= 2)
            return true;

        reverse(postorder.begin(), postorder.end());

        return checkTree(postorder, 0, len - 1);
    }
};

int main()
{
    /* input*/
    vector<int> input = {5, 4, 3, 2, 1};

    /* Test*/
    Solution test;
    bool res = test.verifyPostorder(input);

    return 0;
}
```