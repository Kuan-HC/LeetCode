# 面試金典 1621 T9 鍵盤

在老式手機上，用戶通過數字鍵盤輸入，手機將提供與這些數字相匹配的單詞列表。

每個數字映射到0至4個字母。給定一個數字序列，實現一個算法來返回匹配單詞的列表。你會得到一張含有有效單詞的列表。映射如下圖所示：


## T9

GOn old cell phones, users typed on a numeric keypad and the phone would provide a list of words that matched these numbers. Each digit mapped to a set of 0 - 4 letters. Implement an algo­rithm to return a list of matching words, given a sequence of digits. You are provided a list of valid words. The mapping is shown in the diagram below:

<img src="img/1620.png" width = "240"/>



[LeetCode](https://leetcode-cn.com/problems/t9-lcci)

### Example 1
```
Input: num = "8733", words = ["tree", "used"]
Output: ["tree", "used"]
```

### C++ 


```
class Solution {
private:
    char charTodigit(const char& c)
    {
        int num = c - 'a';
        if(num < 15)
            return (char)num/3 + 50;
        else if(num < 19)
            return '7';
        else if(num < 22)
            return '8';
        else
            return '9';
    }
public:
    vector<string> getValidT9Words(string num, vector<string>& words) {
        
        int len = num.length();
        if (len == 0)
            return {};
        vector<string> ret;    
        
        for( const string& word: words)
        {
            if(word.length() != len)
                continue;

            bool same = true;
            for(int i = 0; i < len; i++)
            {
                if(num[i] != charTodigit(word[i]))
                {
                    same = false;
                    break;
                }
            }
            if(same == true)
                ret.emplace_back(word);
        }
        return ret;
    }
};
```
