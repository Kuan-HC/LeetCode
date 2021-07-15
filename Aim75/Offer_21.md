# 劍指 Offer 28 調整數組順序使奇數位於偶數前面

輸入一個整數數組，實現一個函數來調整該數組中數字的順序，使得所有奇數位於數組的前半部分，所有偶數位於數組的後半部分

[LeetCode](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)



### Example 1

```
輸入：nums = [1,2,3,4]
輸出：[1,3,2,4] 
註：[3,1,2,4] 也是正確的答案之一
```


* 0 <= nums.length <= 50000
* 1 <= nums[i] <= 10000

## Solution  


### C++

* 時間覆雜度: O(n) 

* 空間覆雜度: O(1) 


```
#include <vector>
#include <algorithm>

using namespace std;

class Solution
{
public:
    vector<int> exchange(vector<int> &nums)
    {
        /* set two pointers, left and right, start from each end*/
        int len = nums.size();
        int left = 0;
        int right = len - 1;

        while (left < right)
        {
            while (nums[left] % 2 == 1 && left < right)
                left++;
            while (nums[right] % 2 == 0 && right > left)
                right--;

            if (left < right)
                swap(nums[left++], nums[right--]);
        }

        return nums;
    }
};

int main()
{
    /* input*/
    vector<int> input = {2,4,6};

    /* Test*/
    Solution test;
    vector<int> res = test.exchange(input);

    return 0;
}
```