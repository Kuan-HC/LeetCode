# 面試金典 1002 變位詞組

編寫一種方法，對字符串數組進行排序，將所有變位詞組合在一起。變位詞是指字母相同，但排列不同的字符串。

## Group Anagrams

Write a method to sort an array of strings so that all the anagrams are in the same group.

[LeetCode](https://leetcode-cn.com/problems/group-anagrams-lcci/)

### Example 1
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

### C++ 

```
class Solution
{
public:
    vector<vector<string>> groupAnagrams(vector<string> &strs)
    {
        unordered_map<string, vector<string>> sortWord;

        for (const string &word : strs)
        {
            string copy = word;
            sort(copy.begin(), copy.end());
            sortWord[copy].emplace_back(word);
        }

        vector<vector<string>> ret;
        for (const auto &item : sortWord)
            ret.emplace_back(item.second);

        return ret;
    }
};
```
