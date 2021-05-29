# 005. Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.

[LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)

### Example 1:
```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
### Example 2:
```
Input: s = "cbbd"
Output: "bb"
```
### Example 3:
```
Input: s = "a"
Output: "a"
```
### Example 4:
```
Input: s = "ac"
Output: "a"
```

#  最長回文子串
給定一個字符串，請你找出s中最長的回文子串

## Solution  

### C++

```
#include <string>

using namespace std;

class Solution
{
public:
    string longestPalindrome(string s)
    {
        int sLen = s.size();
        int maxLen = 0;
        int start = 0;

        for (int i = 0; i < sLen; ++i)
        {
            int left = i;
            int right = i;
            int tmpLen = 0;

            /* locate the core */
            while (right + 1 < sLen && s[i] == s[right + 1])
            {
                ++right;
            }

            /* expand from core s[i] */
            while (left >= 0 && right < sLen && s[left] == s[right])
            {
                tmpLen = right - left + 1;
                if (tmpLen > maxLen)
                {
                    maxLen = tmpLen;
                    start = left;
                }
                --left;
                ++right;
            }
        }

        return s.substr(start, maxLen);
    }
};

int main()
{
    /* Input*/
    string input = "bbbc";

    /* unit test*/
    Solution test;
    string res = test.longestPalindrome(input);

    return 0;
}

```

### C

```
char *longestPalindrome(char *s)
{
    int str_len = strlen(s);
    int left, right, start, length = 0;
    
    for (int i = 0; i < str_len; i++)
    {
        left = i - 1;
        right = i + 1;

        while (s[right] == s[i])
        {
            right++;
        }
        while (left >= 0 && s[right] != '\0' && s[left] == s[right])
        {
            left--;
            right++;
        }
        if (right - left - 1 > length)
        {
            length = right - left - 1;
            start = left + 1;
        }
    }
    
    s[start + length] = '\0';
    s += start;
    return s;
}
```


