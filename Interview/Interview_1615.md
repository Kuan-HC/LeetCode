# 面試金典 1615 珠璣妙算

珠璣妙算遊戲（the game of master mind）的玩法如下。

計算機有4個槽，每個槽放一個球，顏色可能是紅色（R）、黃色（Y）、綠色（G）或藍色（B）。例如，計算機可能有RGGB 4種（槽1為紅色，槽2、3為綠色，槽4為藍色）。
作為用戶，你試圖猜出顏色組合。打個比方，你可能會猜YRGB。要是猜對某個槽的顏色，則算一次“猜中”；要是只猜對顏色但槽位猜錯了，則算一次“偽猜中”。注意，“猜中”不能算入“偽猜中”。

給定一種顏色組合solution和一個猜測guess，編寫一個方法，返回猜中和偽猜中的次數answer，其中answer[0]為猜中的次數，answer[1]為偽猜中的次數。

 
[LeetCode](https://leetcode-cn.com/problems/master-mind-lcci/)

### Example 1
```
IInput:  solution="RGBY",guess="GGRR"
Output:  [1,1]
Explanation:  hit once, pseudo-hit once.
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(n)

```
class Solution
{
public:
    vector<int> masterMind(string solution, string guess)
    {
        unordered_map<char, int> stats;
        vector<int> ret(2,0);
       
        for(int i = 0; i < solution.size(); ++i){
            if(solution[i] == guess[i]){    
                ret[0]++;                
            }
            else{
            stats[solution[i]]++;
            }
        }

        for(int i = 0; i < solution.size(); ++i){
            if(solution[i] != guess[i] && stats[guess[i]] != 0){    
                ret[1]++;
                stats[guess[i]]--;
            }
        }

        return ret;
    }
};

int main(void)
{
    /* input*/
    string solution = "RGBY";
    string guess = "GGRR";

    /* test*/
    Solution test;
    vector<int> res = test.masterMind(solution, guess);

    return 0;
}
```
