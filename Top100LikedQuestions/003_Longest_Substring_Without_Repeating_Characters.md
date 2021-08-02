# 003. Longest Substring Without Repeating Characters
Given a string s, find the length of the longest substring without repeating characters.

[LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### Example 1:
```
Input: s = "abcabcbb"
Output: 3
```
### Example 2:
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
### Example 3:
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
### Example 4:
```
Input: s = ""
Output: 0
```

#  無重覆字符的最長子串
給定一個字符串，請你找出其中不含有重覆字符的最長子串的長度

## Solution  
<img src="img/003.JPG" width = "700"/>

### C

```
int lengthOfLongestSubstring(char *s)
{
    int ascii[128];
    memset(ascii, -1, sizeof(ascii));

    int start = 0;
    int max_len = 0;
    int len = strlen(s);

    for (int i = 0; i < len; i++)
    {
        int tmp = ascii[s[i]];
        if (ascii[s[i]] >= start)
        {
            start = ascii[s[i]] + 1;
        }
        ascii[s[i]] = i;
        if ((i - start + 1) > max_len)
            max_len = (i - start + 1);
    }

    return max_len;
}
```
### C++

* 時間複雜度：O(n)  其中 N 為字符串長度

* 空間複雜度：O(1) ： 字符的 ASCII 碼範圍為 0 ~ 127 ，哈希表 dic 最多使用 O(128) = O(1) 大小的額外空間。

```
#include <string>
#include <unordered_map>

using namespace std;

class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {
        int len = s.size();
        if (len <= 1)
            return len;

        int left = 0;
        int right = left;
        int maxLen = 0;

        unordered_map<char, int> letterMap;

        for (; right < len; ++right)
        {
            if (letterMap.find(s[right]) != letterMap.end() && letterMap[s[right]] != -1)
            {
                while (left < letterMap[s[right]] + 1 ) // left move to s[right] last position + 1
                    letterMap[s[left++]] = -1;
            }

            letterMap[s[right]] = right;

            maxLen = right - left + 1 > maxLen ? right - left + 1 : maxLen;
        }

        return maxLen;
    }
};

int main()
{
    /* input*/
    string input = "dvdf";
    /* Test*/
    Solution test;
    int res = test.lengthOfLongestSubstring(input);

    return 0;
}

```

