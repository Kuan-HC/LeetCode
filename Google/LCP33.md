# LCP 33 蓄水

給定 N 個無限容量且初始均空的水缸，每個水缸配有一個水桶用來打水，第 i 個水缸配備的水桶容量記作 bucket[i]。小扣有以下兩種操作：

* 升級水桶：選擇任意一個水桶，使其容量增加為 bucket[i]+1
* 蓄水：將全部水桶接滿水，倒入各自對應的水缸
每個水缸對應最低蓄水量記作 vat[i]，返回小扣至少需要多少次操作可以完成所有水缸蓄水要求。

注意：實際蓄水量 
 

[LeetCode](https://leetcode.cn/problems/o8SXZn/)


### Example 1

```
輸入：bucket = [1,3], vat = [6,8]

輸出：4

解釋： 第 1 次操作升級 bucket[0]； 第 2 ~ 4 次操作均選擇蓄水，即可完成蓄水要求。
```

### Example 2

```
輸入：bucket = [9,0,1], vat = [0,2,2]

輸出：3

解釋： 第 1 次操作均選擇升級 bucket[1] 第 2~3 次操作選擇蓄水，即可完成蓄水要求。
```


### Constraints

* 1 <= bucket.length == vat.length <= 100
* 0 <= bucket[i], vat[i] <= 10^4

### C++ 

```
class Solution {
public:
    int storeWater(vector<int>& bucket, vector<int>& vat) {
        /*
            總共要裝水的次數可能 1 - 最大的水統值
            遍歷x in range (1 - max volum)
            對應水桶要變大
        */

        int maxVol = *max_element(vat.begin(), vat.end());
        if(maxVol == 0)
            return 0;
        
        int ret = INT_MAX;
        for(int i = 1; i <= maxVol; ++i){
            int increase = 0;
            for(int j = 0; j < bucket.size(); ++j){
                increase += max(0, (vat[j] + i - 1) / i - bucket[j]);
            }
            ret = min(ret, increase + i);
        }

        return ret;
    }
};
```