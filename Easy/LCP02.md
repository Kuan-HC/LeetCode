# LCP02 分式化簡

有一個同學在學習分式。他需要將一個連分數化成最簡分數，你能幫助他嗎？

<img src="img/lcp02.jpg" width = "250"/>

連分數是形如上圖的分式。在本題中，所有系數都是大於等於0的整數。

 

輸入的cont代表連分數的系數（cont[0]代表上圖的a0，以此類推）。返回一個長度為2的數組[n, m]，使得連分數的值等於n / m，且n, m最大公約數為1。
 
[LeetCode](https://leetcode.cn/problems/deep-dark-fraction/)

### Example 1

```
輸入：cont = [3, 2, 0, 2]
輸出：[13, 4]
解釋：原連分數等價於3 + (1 / (2 + (1 / (0 + 1 / 2))))。注意[26, 8], [-13, -4]都不是正確答案。
```

### Example 2

```
輸入：cont = [0, 0, 3]
輸出：[3, 1]
解釋：如果答案是整數，令分母為1即可。
```

### Constraints

* cont[i] >= 0
* 1 <= cont的長度 <= 10
* cont最後一個元素不等於0
* 答案的n, m的取值都能被32位int整型存下（即不超過2 ^ 31 - 1）。

### C++ 

```
class Solution {
public:
    vector<int> fraction(vector<int>& cont) {
        /*
            從後往前遍歷數組，分式的最後一項為
            分子 : 1
            分母 = cont[len - 1]

            到第二項時，
            分子變成 前一項中的分母
            分子變成 前一項中的分母 * cont[i] + 前一項中分子
        */

        int son = 1;              //分子
        int parent = cont.back();  //分母

        for(int i = cont.size() - 2; i >= 0; --i){
            int tmp = parent;
            parent = parent * cont[i] + son;
            son = move(tmp);
        }

        return vector<int>{parent, son};
    }
};
```