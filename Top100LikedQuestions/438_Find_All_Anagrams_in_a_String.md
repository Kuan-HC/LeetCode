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
#include <unordered_map>
#include <string>
#include <vector>
#include <iostream>

using namespace std;

class Solution
{

public:
    vector<int> findAnagrams(string s, string p)
    {
        unordered_map<char, int> targetMap;
        unordered_map<char, int> sourceMap;
        vector<int> ret(0);

        int sLength = s.length();
        int pLength = p.length();

        if(pLength > sLength)
            return ret;
        
        for (const char &c : p)
            targetMap[c]++;

        /*sliding windows*/
        int left = 0;
        int right = 0;
        bool identical;
        
        while (right < sLength)
        {
            /** 
             * Add s[right] to the sourceMap
             * also slide right boundary one unit to the right*/
            sourceMap[s[right++]]++;

            if ((right - left) == pLength)
            {
                /*check map*/
                identical = true;
                for (auto key : targetMap)
                {
                    if (sourceMap[key.first] != targetMap[key.first])
                    {
                        identical = false;
                        break;
                    }
                }
                /* record current windows start position in the vector*/
                if (identical == true)
                    ret.push_back(left);

                /**
                 *  remove the most left element from the sourceMap,
                 *  also slide left boundary one step right
                 */
                sourceMap[s[left++]]--;
            }
        }

        return ret;
    }
};

int main()
{
    string input = "aabb";
    string target = "bb";

    Solution test;
    vector<int> res = test.findAnagrams(input, target);

    for (int &i : res)
        cout << i << ' ';
    cout << endl;

    return 0;
}
```