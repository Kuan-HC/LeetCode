# LCP 01 Latest Time You Can Obtain After Replacing Characters

小A 和 小B 在玩猜數字。小B 每次從 1, 2, 3 中隨機選擇一個，小A 每次也從 1, 2, 3 中選擇一個猜。他們一共進行三次這個遊戲，請返回 小A 猜對了幾次？

輸入的guess數組為 小A 每次的猜測，answer數組為 小B 每次的選擇。guess和answer的長度都等於3。
 

[LeetCode](https://leetcode.cn/problems/guess-numbers/)


### Example 1

```
輸入：guess = [1,2,3], answer = [1,2,3]
輸出：3
解釋：小A 每次都猜對了。
```

### Example 2

```
輸入：guess = [2,2,3], answer = [3,2,1]
輸出：1
解釋：小A 只猜對了第二次。
```


### Constraints

* guess 的長度 = 3
* answer 的長度 = 3
* guess 的元素取值為 {1, 2, 3} 之一。
* answer 的元素取值為 {1, 2, 3} 之一。

### C++ 

```
class Solution {
public:
    int game(vector<int>& guess, vector<int>& answer) {
        int ret = 0;
        for(int i = 0; i < guess.size(); ++i){
            if(guess[i] == answer[i])
                ++ret;
        }

        return ret;
    }
};
```