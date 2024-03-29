# 053. Maximum Subarray
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

##  最大子序和
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

[LeetCode](https://leetcode.com/problems/two-sum/)  

### Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

### Example 2:
```
Input: nums = [1]
Output: 1
```

# 最大子序和
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。  

## Solution
<img src="img/53.jpg" width = "500"/>

### C++

* Caterpillar Method

* 時間複雜度 O(n)

* 空間複雜度 O(1)

```
#include <vector>
#include <climits>

using namespace std;

class Solution
{
public:
    int maxSubArray(vector<int> &nums)
    {
        int len = nums.size();

        /* caterpillar method*/
        int head = 0;
        int tail = 0;
        int tmpSum = 0;
        int maxSum = INT_MIN;
        while (head < len)
        {
            tmpSum += nums[head];

            maxSum = max(tmpSum, maxSum);

            if(tmpSum < 0)
            {
                tmpSum = 0;
                tail = head;
            }
             head++;
        }
       

        return maxSum;
    }
};

int main()
{
    /* Input*/
    vector<int> input = {-2, 1, -3, 4, -1, 2, 1, -5, 4};

    /* unit test*/
    Solution test;
    bool res = test.maxSubArray(input);

    return 0;
}
```

### C
```
int maxSubArray(int* nums, int numsSize){
    
    int tmp_max = nums[0]; 
    int sum = 0;
    for(int i = 0; i < numsSize; i++){
        sum += nums[i];
        tmp_max = (sum > tmp_max? sum:tmp_max);
        if (sum < 0)
            sum = 0;
                           
    }

    return tmp_max;
}
```




