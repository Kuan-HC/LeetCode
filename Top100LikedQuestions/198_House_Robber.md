# 198. House Robber
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

[LeetCode](https://leetcode.com/problems/house-robber/)

### Example 1:
```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

### Example 2:
```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```
### Constraints
```
0 <= nums.length <= 100
0 <= nums[i] <= 400
```


# 打家劫舍
你是一個專業的小偷，計劃偷竊沿街的房屋。每間房內都藏有一定的現金，影響你偷竊的唯一制約因素就是相鄰的房屋裝有相互連通的防盜系統，如果兩間相鄰的房屋在同一晚上被小偷闖入，系統會自動報警。

給定一個代表每個房屋存放金額的非負整數數組，計算你 不觸動警報裝置的情況下 ，一夜之內能夠偷竊到的最高金額。


# Solution  
## Dynamic Programming
  
[Wiki](https://zh.m.wikipedia.org/zh-tw/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
動態規劃背後的基本思想非常簡單。大致上，若要解一個給定問題，我們需要解其不同部分（即子問題），再根據子問題的解以得出原問題的解。  

通常許多子問題非常相似，為此動態規劃法試圖僅僅解決每個子問題一次，從而減少計算量：一旦某個給定子問題的解已經算出，則將其記憶化儲存，  
以便下次需要同一個子問題解之時直接查表。這種做法在重複子問題的數目關於輸入的規模呈指數增長時特別有用

## C

```
#define MAX(a,b) a > b? a:b

int rob(int* nums, int numsSize){
    if( nums == NULL || numsSize == 0)
        return 0;

    if(numsSize == 1)    
        return nums[0];
    else if(numsSize == 2)
        return MAX(nums[0],nums[1]);

    int dp_minus_2 = nums[0];
    int dp_minus_1 = MAX(nums[0], nums[1]);
    int tmp_dp = 0;

    for(int i = 2; i < numsSize; i++){
        tmp_dp = MAX(dp_minus_2 + nums[i], dp_minus_1);
        dp_minus_2 = dp_minus_1;
        dp_minus_1 = tmp_dp;
    }

    return tmp_dp;
}
```


