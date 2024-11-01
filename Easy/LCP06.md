# LCP06 分式化簡

桌上有 n 堆力扣幣，每堆的數量保存在數組 coins 中。我們每次可以選擇任意一堆，拿走其中的一枚或者兩枚，求拿完所有力扣幣的最少次數
 
[LeetCode](https://leetcode.cn/problems/na-ying-bi/)

### Example 1

```
輸入：[4,2,1]

輸出：4

解釋：第一堆力扣幣最少需要拿 2 次，第二堆最少需要拿 1 次，第三堆最少需要拿 1 次，總共 4 次即可拿完。
```

### Example 2

```
輸入：[2,3,10]

輸出：8
```

### Constraints

* 1 <= n <= 4
* 1 <= coins[i] <= 10

### C++ 

```
class Solution {
public:
    int minCount(vector<int>& coins) {
        int ret = 0;
        for(const int& num : coins){
             ret += num >> 1;
            if(num & 1)
                ++ret;                
        }

        return ret;        
    }
};
```