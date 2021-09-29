# 面試金典 1715 最長單詞

給定一組單詞words，編寫一個程序，找出其中的最長單詞，且該單詞由這組單詞中的其他單詞組合而成。
若有多個長度相同的結果，返回其中字典序最小的一項，若沒有符合要求的單詞則返回空字符串。

## Longest Word

Given a list of words, write a program to find the longest word made of other words in the list. 
If there are more than one answer, return the one that has smallest lexicographic order. 
If no answer, return an empty string.
 
[LeetCode](https://leetcode-cn.com/problems/longest-word-lcci/)

### Example 1
```
Input:  ["cat","banana","dog","nana","walk","walker","dogwalker"]
Output:  "dogwalker"
Explanation:  "dogwalker" can be made of "dog" and "walker".

```

### C++ 


```
class Trie
{
public:
    bool isEnd{false};
    Trie *next[26]{nullptr};

    void insert(string s)
    {
        Trie *currPos = this;
        int num = 0;
        for (const auto &c : s)
        {
            num = c - 'a';
            if (currPos->next[num] == nullptr)
                currPos->next[num] = new Trie();
            currPos = currPos->next[num];
        }
        currPos->isEnd = true;
    }
};

class Solution
{
private:
    static bool comp(const string &lhs, const string &rhs)
    {
        if (lhs.length() != rhs.length())
            return lhs.length() > rhs.length();

        return lhs < rhs;
    }

public:
    string longestWord(vector<string> &words)
    {

        /* 建立字典樹 Trie */
        Trie *wordTree = new Trie();
        for (const string &word : words)
            wordTree->insert(word);

        /* 符合題目要求的檢查順序，一找到就可以退出即為答案*/
        sort(words.begin(), words.end(), comp);

        int num = 0;
        for (const string &word : words)
        {
            int len = word.length();
            vector<int> dp(len + 1, 0);
            dp[0] = 1; // 可以開始的位置設置為正數，最後一格-1即可知由幾個字組成
            for (int i = 1; i <= len; ++i)
            {
                if(dp[i - 1 ] == 0)
                    continue;

                Trie *root = wordTree;
                for (int j = i; j <= len; ++j)
                {
                    num = word[j - 1] - 'a';
                    if (root->next[num] == nullptr)
                        break;
                    else if (root->next[num]->isEnd == true)
                        dp[j] = dp[i - 1] + 1;
                    root = root->next[num];
                }
            }
            if(dp[len] - 1 > 1)
                return word;
        }

        return "";
    }
};

int main(void)
{
    /* input*/
    vector<string> dictionary = {"ttaaaa","pp","tpa","kpaqkt","tktpqq","aqppatp"};

    Solution test;
    string res = test.longestWord(dictionary);

    return 0;
}
```
