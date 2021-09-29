# 面試金典 1712 恢復空格

哦，不！你不小心把一個長篇文章中的空格、標點都刪掉了，並且大寫也弄成了小寫。像句子"I reset the computer. It still didn’t boot!"已經變成了"iresetthecomputeritstilldidntboot"。在處理標點符號和大小寫之前，你得先把它斷成詞語。當然了，你有一本厚厚的詞典dictionary，不過，有些詞沒在詞典里。假設文章用sentence表示，設計一個算法，把文章斷開，要求未識別的字符最少，返回未識別的字符數。

注意：本題相對原題稍作改動，只需返回未識別的字符數

## Re-Space

Oh, no! You have accidentally removed all spaces, punctuation, and capitalization in a lengthy document. A sentence like "I reset the computer. It still didn't boot!" became "iresetthecomputeritstilldidntboot''. You'll deal with the punctuation and capi­talization later; right now you need to re-insert the spaces. Most of the words are in a dictionary but a few are not. Given a dictionary (a list of strings) and the document (a string), design an algorithm to unconcatenate the document in a way that minimizes the number of unrecognized characters. Return the number of unrecognized characters.
 
[LeetCode](https://leetcode-cn.com/problems/re-space-lcci/)

### Example 1
```
Input: 
dictionary = ["looked","just","like","her","brother"]
sentence = "jesslookedjustliketimherbrother"
Output:  7
Explanation:  After unconcatenating, we got "jess looked just like tim her brother", which containing 7 unrecognized characters.
```

### C++ 

* 時間複雜度 O(N)

* 空間複雜度 O(N)

```
#include <vector>
#include <string>

using namespace std;
class Trie
{
public:
    bool isEnd{false};
    Trie *next[26]{nullptr};

    void insert(string word)
    {
        Trie *root = this;
        int num = 0;
        int len = word.size();
        for (int i = len - 1; i >= 0; --i)
        {
            num = word[i] - 'a';
            if (root->next[num] == nullptr)
                root->next[num] = new Trie();

            root = root->next[num];
        }
        root->isEnd = true;
    }
};

class Solution
{
public:
    int respace(vector<string> &dictionary, string sentence)
    {
        int len = sentence.size();
        if (len == 0)
            return 0;
        Trie *wordTree = new Trie();
        /* 將字典中的字變成字典樹*/
        for (const string &word : dictionary)
            wordTree->insert(word);

        /* 動態規劃*/
        vector<int> dp(len + 1, 0);
        int num = 0;
        for (int i = 1; i <= len; i++)
        {
            dp[i] = dp[i - 1] + 1; //預設這個字符找不到對應的
            Trie *root = wordTree;

            for (int j = 0; j < i; j++)
            {
                num = sentence[i - 1 - j] - 'a';
                if (root->next[num] == nullptr)
                    break;
                if (root->next[num]->isEnd == true)
                    dp[i] = min(dp[i], dp[i - j - 1]);
                root = root->next[num];
            }
        }

        return dp[len];
    }
};

int main(void)
{
    /* input*/
    vector<string> dictionary = {"looked", "just", "like", "her", "brother"};
    string sentence = "jesslookedjustliketimherbrother";

    Solution test;
    int res = test.respace(dictionary, sentence);

    return 0;
}
```
