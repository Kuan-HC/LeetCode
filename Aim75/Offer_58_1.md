# 劍指 Offer 58-1 翻轉單詞順序

輸入一個英文句子，翻轉句子中單詞的順序，但單詞內字符的順序不變。為簡單起見，標點符號和普通字母一樣處理。例如輸入字符串"I am a student. "，則輸出"student. a am I"。

[LeetCode](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

### Example 1
```
輸入: "the sky is blue"
輸出: "blue is sky the"
```

### Example 2
```
輸入: "  hello world!  "
輸出: "world! hello"
解釋: 輸入字符串可以在前面或者後面包含多余的空格，但是反轉後的字符不能包括。
```

### Example 3
```
輸入: "a good   example"
輸出: "example good a"
解釋: 如果兩個單詞間有多余的空格，將反轉後單詞間的空格減少到只含一個。
```

* 無空格字符構成一個單詞。
* 輸入字符串可以在前面或者後面包含多余的空格，但是反轉後的字符不能包括。


## Solution  

### C++

* 時間複雜度：O(N) 指標left需要從最右邊走到最左邊，為string 長度 N

* 空間複雜度：O(1) 
```
#include <string>

using namespace std;

class Solution
{
public:
    string reverseWords(string s)
    {
        int len = s.size();
        if (len == 0)
            return s;

        int left = len - 1;
        int right = left;
        string ret;

        /* two pointers start from the end of string*/
        while (left >= 0)
        {
            if (s[left] == ' ' && s[right] == ' ')
            {
                left--;
                right--;
            }
            else if ((left == 0 || s[left] == ' ') && s[right] != ' ')
            {
                string tmp = s.substr(left, right - left + 1);
                if (tmp[0] != ' ')
                    tmp =  " " + tmp;
                ret += tmp;
                right = --left;
            }
            else if (s[left] != ' ' && s[right] != ' ')
                left--;
        }

        if (ret[0] == ' ')
            ret = ret.substr(1, ret.size() - 1);

        return ret;
    }
};

int main()
{
    /* input*/
    string input = "   f  j";

    /* Test*/
    Solution test;
    string res = test.reverseWords(input);

    return 0;
}
```
### C++

```
#include <vector>
#include <string>

using namespace std;

class Solution
{
public:
    string reverseWords(string s)
    {
        vector<string> buffer;
        string tempS;
        for (const char &c : s)
        {
            if (c == ' ')
            {
                if (tempS.size() > 0)
                {
                    buffer.emplace_back(tempS);
                    tempS.clear();
                }
                continue;
            }
            tempS += c;
        }
        if (tempS.size() > 0)
            buffer.emplace_back(tempS);

        /* build string from vector*/
        tempS.clear();
        for (auto it = buffer.rbegin(); it != buffer.rend(); it++)
        {
            if (it == buffer.rbegin())
                tempS += *it;
            else
                tempS = tempS + ' ' + *it;
        }
        return tempS;
    }
};

int main()
{
    /* input*/
    string input = "  hello world!  ";

    /* Test*/
    Solution test;
    string res = test.reverseWords(input);

    return 0;
}
```