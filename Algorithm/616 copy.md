# 616 給字符串添加加粗標簽

給你一個字符串 s 和一個字符串列表 words ，你需要將在字符串列表中出現過的 s 的子串添加加粗閉合標簽 <b> 和 </b> 。

如果兩個子串有重疊部分，你需要把它們一起用一對閉合標簽包圍起來。同理，如果兩個子字符串連續被加粗，那麽你也需要把它們合起來用一對加粗標簽包圍。

返回添加加粗標簽後的字符串 s 。


##  Add Bold Tag in String

You are given a string s and an array of strings words. You should add a closed pair of bold tag <b> and </b> to wrap the substrings in s that exist in words. 
If two such substrings overlap, you should wrap them together with only one pair of closed bold-tag. 
If two substrings wrapped by bold tags are consecutive, you should combine them.

Return s after adding the bold tags.



[LeetCode](https://leetcode-cn.com/add-bold-tag-in-string/)

### Example 1

```
Input: s = "abcxyz123", words = ["abc","123"]
Output: "<b>abc</b>xyz<b>123</b>"
```

### Example 2

```
Input: s = "aaabbcc", words = ["aaa","aab","bc"]
Output: "<b>aaabbc</b>c"
```
### C++ 

```
class Solution {

public:
    string addBoldTag(string s, vector<string>& words) {
        int&& sLen = s.length();
        //紀錄哪些位置為變成粗體
        vector<bool> record(sLen, false);
        for(const string& word : words)
        {
            int&& start = 0;    
            int&& wordLen = word.length();        
            while((start = s.find(word, start)) != string::npos )
            {
                for(int i = 0; i < wordLen; ++i)
                    record[start + i] = true;
                ++start;// = s.find(word, start + 1);
            }
        } 
              
        string ret;
        for(int i = 0; i < sLen; ++i)
        {
            if(record[i] == true && (i == 0 || record[i - 1] == false))
                ret += "<b>";
            ret += s[i];
            if(record[i] == true && (i == sLen - 1 || record[i + 1] != true))
                ret += "</b>";
        }
        return ret;
    }
};
```
