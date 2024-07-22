# LCP 07 傳遞信息

小朋友 A 在和 ta 的小夥伴們玩傳信息遊戲，遊戲規則如下：

有 n 名玩家，所有玩家編號分別為 0 ～ n-1，其中小朋友 A 的編號為 0
每個玩家都有固定的若幹個可傳信息的其他玩家（也可能沒有）。傳信息的關系是單向的（比如 A 可以向 B 傳信息，但 B 不能向 A 傳信息）。
每輪信息必須需要傳遞給另一個人，且信息可重覆經過同一個人
給定總玩家數 n，以及按 [玩家編號,對應可傳遞玩家編號] 關系組成的二維數組 relation。返回信息從小 A (編號 0 ) 經過 k 輪傳遞到編號為 n-1 的小夥伴處的方案數；若不能到達，返回 0。
 

[LeetCode](https://leetcode.cn/problems/chuan-di-xin-xi/)


### Example 1

```
輸入：n = 5, relation = [[0,2],[2,1],[3,4],[2,3],[1,4],[2,0],[0,4]], k = 3

輸出：3

解釋：信息從小 A 編號 0 處開始，經 3 輪傳遞，到達編號 4。共有 3 種方案，分別是 0->2->0->4， 0->2->1->4， 0->2->3->4。
```

### Example 2

```
輸入：n = 3, relation = [[0,2],[2,1]], k = 2

輸出：0

解釋：信息不能從小 A 處經過 2 輪傳遞到編號 2
```


### Constraints

* 2 <= n <= 10
* 1 <= k <= 5
* 1 <= relation.length <= 90, 且 relation[i].length == 2
* 0 <= relation[i][0],relation[i][1] < n 且 relation[i][0] != relation[i][1]

### C++ 

```
class Solution {
public:
    int numWays(int n, vector<vector<int>>& relation, int k) {
        vector<int> prevDp(n);
        vector<int> dp(n);
        prevDp[0] = 1;

        for(int i = 0; i < k; ++i){
            dp.resize(n);
            for(const vector<int>& array : relation){
                dp[array[1]] += prevDp[array[0]];
            }
            prevDp = move(dp);
        }

        return prevDp.back();
    }
};
```