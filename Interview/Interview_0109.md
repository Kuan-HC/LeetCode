# 面試金典 0109 字符串輪轉

字符串輪轉。給定兩個字符串s1和s2，請編寫代碼檢查s2是否為s1旋轉而成（比如，waterbottle是erbottlewat旋轉後的字符串）。

[LeetCode](https://leetcode-cn.com/problems/string-rotation-lcci/)

### Example 1
```
 輸入：s1 = "waterbottle", s2 = "erbottlewat"
 輸出：True
```

### Example 2
```
 輸入：s1 = "aa", s2 = "aba"
 輸出：False
```

* 字符串長度在[0, 100000]範圍內。

說明:

你能只調用一次檢查子串的方法嗎？

### C++

* 時間複雜度：o(1) 

* 空間複雜度：o(1) 

```
#include <string>

using namespace std;

class Solution
{
public:
    bool isFlipedString(string s1, string s2)
    {
        if(s1.size() != s2.size())
            return false;

        s1 += s1;

        return s1.find(s2) == -1? false: true;
    }
};

int main()
{
    /* input*/
    string input1 = "waterbottle";
    string input2 = "erbottlewat";

    /* Test*/
    Solution test;
    bool res = test.isFlipedString(input1, input2);

    return 0;
}
```
