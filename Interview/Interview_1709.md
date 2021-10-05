# 面試金典 1709 第K個數

有些數的素因子只有 3，5，7，請設計一個算法找出第 k 個數。

注意，不是必須有這些素因子，而是必須不包含其他的素因子。例如，前幾個數按順序應該是 1，3，5，7，9，15，21。

## Get Kth Magic Number 

Design an algorithm to find the kth number such that the only prime factors are 3, 5, and 7. Note that 3, 5, and 7 do not have to be factors, but it should not have any other prime factors. For example, the first several multiples would be (in order) 1, 3, 5, 7, 9, 15, 21.

[LeetCode](https://leetcode-cn.com/problems/get-kth-magic-number-lcci)

### Example 1
```
Input: k = 5

Output: 9
```

### C++ 

```
class Solution {
public:
    int getKthMagicNumber(int k) {
        /* three pointer*/
        vector<int> list (k+1);
        list[1] = 1;

        int pt3 = 1;
        int pt5 = 1;
        int pt7 = 1;

        for(int i = 2; i <= k; i++)
        {   int product3 = list[pt3] * 3;
            int product5 = list[pt5] * 5;
            int product7 = list[pt7] * 7;
            list[i] = min({product3, product5, product7});

            if(list[i] == product3)
                pt3++;
            if(list[i] == product5)
                pt5++;
            if(list[i] == product7)
                pt7++;
        }

        return list[k];
    }
};

```
