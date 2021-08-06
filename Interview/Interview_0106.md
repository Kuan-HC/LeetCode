# 面試金典 0106 字符串壓縮

字符串壓縮。利用字符重覆出現的次數，編寫一種方法，實現基本的字符串壓縮功能。比如，字符串aabcccccaaa會變為a2b1c5a3。
若“壓縮”後的字符串沒有變短，則返回原先的字符串。你可以假設字符串中只包含大小寫英文字母（a至z）。

[LeetCode](https://leetcode-cn.com/problems/compress-string-lcci/)

### Example 1
```
 輸入："aabcccccaaa"
 輸出："a2b1c5a3"
```

### Example 2
```
 輸入："abbccd"
 輸出："abbccd"
 解釋："abbccd"壓縮後為"a1b2c2d1"，比原字符串長度更長。
```

* 字符串長度在[0, 50000]範圍內。

### C++

* 時間複雜度：o(n) string的長度

* 空間複雜度：o(1) ret反回，故不記入空間複雜度

```
#include <string>

using namespace std;

class Solution
{
public:
    string compressString(string S)
    {

        int len = S.size();

        if (len == 0)
            return S;

        char key = S[0];
        int count = 0;
        string ret;

        for (int i = 0; i < len; ++i)
        {
            if (S[i] != key)
            {
                ret += key;
                ret += to_string(count);
                key = S[i];
                count = 0;
            }
            ++count;
        }
        ret += key;
        ret += to_string(count);

        return ret.size() >= len? S:ret;
    }
};

int main()
{
    /* input*/
    string input = "aabcccccaaa";

    /* Test*/
    Solution test;
    string res = test.compressString(input);

    return 0;
}
```
