# 劍指 Offer 48 最長不含重覆字符的子字符串

請從字符串中找出一個最長的不包含重覆字符的子字符串，計算該最長子字符串的長度。

[LeetCode](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/) 

### Example 1
```
輸入: "abcabcbb"
輸出: 3 
解釋: 因為無重覆字符的最長子串是 "abc"，所以其長度為 3。
```

### Example 2
```
輸入: "bbbbb"
輸出: 1
解釋: 因為無重覆字符的最長子串是 "b"，所以其長度為 1。
```

### Example 3
```
輸入: "pwwkew"
輸出: 3
解釋: 因為無重覆字符的最長子串是 "wke"，所以其長度為 3。
     請注意，你的答案必須是 子串 的長度，"pwke" 是一個子序列，不是子串。
```
 
* s.length <= 40000

## Solution  


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