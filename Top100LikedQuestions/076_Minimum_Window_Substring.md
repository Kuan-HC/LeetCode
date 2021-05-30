# 076. Minimum Window Substring

Given two strings s and t of lengths m and n respectively, return the minimum window in s which will contain all the characters in t. If there is no such window in s that covers all characters in t, return the empty string "".

Note that If there is such a window, it is guaranteed that there will always be only one unique minimum window in s.

[LeetCode](https://leetcode.com/problems/minimum-window-substring)  

### Example 1:

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

### Example 2:

```
Input: s = "a", t = "a"
Output: "a"
```

### Constraints:

* m == s.length
* n == t.length
* 1 <= m, n <= 10^5
* s and t consist of English letters.


# 76. 最小覆蓋子串

給你一個字符串 s 、一個字符串 t 。返回 s 中涵蓋 t 所有字符的最小子串。如果 s 中不存在涵蓋 t 所有字符的子串，則返回空字符串 "" 。

注意：如果 s 中存在這樣的子串，我們保證它是唯一的答案。

## Solution
* Sliding window

<img src="img/076.gif" width = "600"/>

[Leetcode Solution](https://leetcode-cn.com/problems/minimum-window-substring/solution/zui-xiao-fu-gai-zi-chuan-by-leetcode-solution/)

### C++

```
#include <string>
#include <unordered_map>

using namespace std;

class Solution
{
private:
    bool check(unordered_map<char, int> &source, unordered_map<char, int> &target) const
    {
        for (const auto &item : target)
        {
            if (source[item.first] < item.second)
                return false;
        }

        return true;
    }

public:
    string minWindow(string s, string t)
    {
        unordered_map<char, int> target, source;

        /* build t harsh table*/
        for (const auto &c : t)
            target[c]++;

        int left = 0;
        int right = 0;
        int sLen = s.size();

        int outputLeft = -1;
        int outputLen = INT_MAX;

        while (right < sLen)
        {
            source[s[right++]]++;

            while (check(source, target) == true)
            {
                if (right - left < outputLen)
                {
                    outputLen = right - left;
                    outputLeft = left;
                }

                source[s[left++]]--;
            }
        }

        return outputLeft == -1 ? string() : s.substr(outputLeft, outputLen);
    }
};

int main()
{
    /* Input*/
    string source = "ADOBECODEBANC"; 
    string target = "A";

    /* unit test*/
    Solution test;
    string res = test.minWindow(source, target);

    return 0;
}
```