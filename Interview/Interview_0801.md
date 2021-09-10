# 面試金典 0801 三步問題

三步問題。有個小孩正在上樓梯，樓梯有n階台階，小孩一次可以上1階、2階或3階。實現一種方法，計算小孩有多少種上樓梯的方式。結果可能很大，你需要對結果模1000000007。

##  Three Steps Problem 

A child is running up a staircase with n steps and can hop either 1 step, 2 steps, or 3 steps at a time. Implement a method to count how many possible ways the child can run up the stairs. The result may be large, so return it modulo 1000000007.

[LeetCode](https://leetcode-cn.com/problems/three-steps-problem-lcci)


### Example 1
```
輸入：n = 3 
輸出：4
說明: 有四種走法
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(1)

```
class Solution {
public:
    int waysToStep(int n)
    {
        if(n <= 2)
            return n;
        
        long prevOne = 2;
        long prevTwo = 1;
        long prevThr = 1;
        long temp = 0;

        for(int i = 3; i <= n; ++i)
        {
            temp = (prevOne + prevTwo + prevThr) % 1000000007;

            prevThr = prevTwo % 1000000007;
            prevTwo = prevOne % 1000000007;
            prevOne = temp % 1000000007;          
        }
        
        return temp;
    }
};
```
