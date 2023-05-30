# 438. Find All Anagrams in a String
Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order

[LeetCode](https://leetcode.com/problems/find-all-anagrams-in-a-string)

### Example 1:

```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

### Example 2:

```
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```
### Constraints:

* 1 <= s.length, p.length <= 3 * 10^4
* s and p consist of lowercase English letters.


#  找到字符串中所有字母異位詞
給定一個字符串 s 和一個非空字符串 p，找到 s 中所有是 p 的字母異位詞的子串，返回這些子串的起始索引。

字符串只包含小寫英文字母，並且字符串 s 和 p 的長度都不超過 20100。

## Solution  

### C++
* unordered map
* sliding window

```
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        /*
            滑動窗口
            1. 先統計p中的字母的出現次數在unordered_map中，令gap = p.length()
            2. 以滑動窗口，若新的字母在unorder_map中次數不為 0, --gap
            3. 當gap為0時，縮小窗口
        */
        vector<int> ret;
        if(p.length() > s.length())
            return ret;

        int&& gap = p.length();
        unordered_map <char, int> cnt;
        for(const char& chr : p)
            cnt[chr]++;

        //滑動窗口
        int lPtr = 0;
        for(int i = 0; i < s.length(); ++i){
            const char& tmpChr = s[i];
            if(cnt.find(tmpChr) != cnt.end()){
                if(--cnt[tmpChr] >= 0)
                    --gap;
            }

            while(gap == 0){
                if(i - lPtr + 1 == p.length())
                    ret.push_back(lPtr);

                const char& lChr = s[lPtr++];
                if(cnt.find(lChr) != cnt.end()){
                    if(++cnt[lChr] > 0)
                        ++gap;
                }
            }
        }
        
        return ret;

    }
};
```