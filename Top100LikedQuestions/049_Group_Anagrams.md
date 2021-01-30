# 049. Group Anagrams

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

[LeetCode](https://leetcode.com/problems/group-anagrams)  

### Example 1:

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

### Example 2:
```
Input: strs = [""]
Output: [[""]]
```

#  字母異位詞分組
給定一個字符串數組，將字母異位詞組合在一起。字母異位詞指字母相同，但排列不同的字符串。

## Solution
Hash Table
### C++

```
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>
#include <algorithm>

using namespace std;

class Solution
{
public:
    vector<vector<string>> groupAnagrams(vector<string> &strs)
    {
        unordered_map<string, vector<string>> umap;
        for (const auto &input : strs)
        {
            auto sortInput = input;
            sort(sortInput.begin(), sortInput.end());
            umap[sortInput].push_back(input);
        }

        vector<vector<string>> ret;
        for (const auto &row : umap)
        {
            ret.push_back(row.second);
        }

        return ret;
    }
};

int main()
{
    vector<string> input = {"eat", "tea", "tan", "ate", "nat", "bat"};

    Solution test;
    vector<vector<string>> ans = test.groupAnagrams(input);

    for (const auto &row : ans)
    {
        for (const auto i : row)
            cout << i << " ";
        cout << endl;
    }

    return 0;
}
```
