# 面試金典 0807 無重覆字符串的排列組合

編寫一種方法，計算某字符串的所有排列組合，字符串每個字符均不相同。
 
##  Permutation

Write a method to compute all permutations of a string of unique characters.


[LeetCode](https://leetcode-cn.com/problems/permutation-i-lcci/)


### Example 1

```
 Input: S = "qwe"
 Output: ["qwe", "qew", "wqe", "weq", "ewq", "eqw"]
```

### Example 2

```
 Input: S = "ab"
 Output: ["ab", "ba"]
```

### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(n)

```
#include <string>
#include <vector>

using namespace std;

class Solution
{
private:
    vector<string> ret;
    vector<bool> usedChar;
    void dfs(const string &S, string &combination, int &leftVal)
    {
        if (leftVal == 0)
        {
            ret.push_back(combination);
            return;
        }

        int len = S.size();
        for (int i = 0; i < len; ++i)
        {
            if (usedChar[i] == true)
                continue;

            usedChar[i] = true;
            combination += S[i];
            leftVal--;
            dfs(S, combination, leftVal);
            combination.erase(combination.end() - 1);
            leftVal++;
            usedChar[i] = false;
            printf("pause");
        }
    }

public:
    vector<string> permutation(string S)
    {
        int len = S.size();
        if (len == 1)
            return vector<string>{S};

        usedChar.resize(len, false);
        string combination = "";

        dfs(S, combination, len);

        return ret;
    }
};

int main(void)
{
    /* input*/
    string input = "qwe";

    /* test*/

    Solution test;
    vector<string> res = test.permutation(input);

    return 0;
}
```
