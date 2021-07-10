# 劍指 Offer 05 替換空格


 
[LeetCode](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

例如，在下面的 3×4 的矩陣中包含單詞 "ABCCED"（單詞中的字母已標出）。

<img src="img/12_q.jpg" width = "450"/>


### Example 1
```
輸入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
輸出：true
```

* 1 <= s的長度 <= 10000


## Solution  


### C++

* 時間覆雜度 O(n))

* 空間覆雜度 O(n)

```
#include <string>

using namespace std;

class Solution
{
public:
    string replaceSpace(string s)
    {
        string res;

        for (const auto &c : s)
        {
            if (c == ' ')
                res += "%20";
            else
                res += c;
        }

        return res;
    }
};

int main()
{
    /* Input */
    string input = "We are happy.";

    /* Test*/
    Solution test;
    string res = test.replaceSpace(input);

    return 0;
}
```
