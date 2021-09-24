# 面試金典 0105 一次編輯

字符串有三種編輯操作:插入一個字符、刪除一個字符或者替換一個字符。 
給定兩個字符串，編寫一個函數判定它們是否只需要一次(或者零次)編輯。

## One Away

There are three types of edits that can be performed on strings: insert a character, remove a character, or replace a character. Given two strings, write a function to check if they are one edit (or zero edits) away.

 
[LeetCode](https://leetcode-cn.com/problems/one-away-lcci/)

### Example 1
```
Input: 
first = "pale"
second = "ple"
Output: True
```


### C++ 

* 時間複雜度 O( m * n )

* 空間複雜度 O( m * n )

```
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

class Solution
{
public:
    bool oneEditAway(string first, string second)
    {
        int firstLen = first.size();
        int secondLen = second.size();

        /* dynamic programming*/
        vector<vector<int>> dpSpace(secondLen + 1, vector<int>(firstLen + 1, 0));
        for (int i = 0; i < secondLen + 1; i++)
        {
            for (int j = 0; j < firstLen + 1; j++)
            {
                /* initialize the dpspace below*/
                if (i == 0 || j == 0)
                    dpSpace[i][j] = i == 0 ? j : i;
                else if (first[j - 1] == second[i - 1])
                    dpSpace[i][j] = dpSpace[i - 1][j - 1];
                else
                    dpSpace[i][j] = min({dpSpace[i - 1][j - 1], dpSpace[i - 1][j], dpSpace[i][j - 1]}) + 1;
            }
        }
        return dpSpace[secondLen][firstLen] == 1 || dpSpace[secondLen][firstLen] == 0;
    }
};

int main(void)
{
    int show = min(4, 9);
    /* input*/
    string input = "pale";
    string input2 = "pal";
    /* test*/
    Solution test;
    bool res = test.oneEditAway(input, input2);

    return 0;
}
```
