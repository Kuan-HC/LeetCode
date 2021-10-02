# 面試金典 1722 單詞轉換

給定字典中的兩個詞，長度相等。寫一個方法，把一個詞轉換成另一個詞， 但是一次只能改變一個字符。每一步得到的新詞都必須能在字典中找到。

編寫一個程序，返回一個可能的轉換序列。如有多個可能的轉換序列，你可以返回任何一個。

## Word Transformer

Given two words of equal length that are in a dictionary, write a method to transform one word into another word by changing only one letter at a time. The new word you get in each step must be in the dictionary.

Write code to return a possible transforming sequence. If there is more than one sequence, return any of them.

[LeetCode](https://leetcode-cn.com/problems/word-transformer-lcci)

### Example 1
```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output:
["hit","hot","dot","lot","log","cog"]

```

### C++ 


```
class Solution
{
private:
    int wordLen{0};
    unordered_map<string, vector<string>> links;
    vector<string> finalPath;
    bool found{false};

    void buildLinks(const vector<string> &wordList)
    {
        int len = wordList.size();
        int counter = 0;
        for (int i = 0; i < len; i++)
        {
            for (int j = i + 1; j < len; j++)
            {
                counter = 0;
                for (int k = 0; k < wordLen; k++)
                {
                    if (wordList[i][k] != wordList[j][k])
                        counter++;
                }

                if (counter == 1)
                {
                    links[wordList[i]].emplace_back(wordList[j]);
                    links[wordList[j]].emplace_back(wordList[i]);
                }
            }
        }
    }

    void dfs(const string &start, const string &target, unordered_set<string> &pathSet, vector<string> &path)
    {
        if(found == true)
            return;
        
        if (start == target)
        {
            finalPath = path;
            found = true;
            return;
        }

        /* next sting*/
        for (const string &word : links[start])
        {
            if (pathSet.find(word) != pathSet.end())
                continue;

            pathSet.insert(word);
            path.emplace_back(word);
            dfs(word, target, pathSet, path);
            path.pop_back();
        }
    }

public:
    vector<string> findLadders(string beginWord, string endWord, vector<string> &wordList)
    {
        /* create connection*/
        wordList.emplace_back(beginWord);
        wordLen = beginWord.length();
        buildLinks(wordList);

        if (links[endWord].size() == 0)
            return {};

        /* breadth search first algorithm*/
        unordered_set<string> pathSet;
        vector<string> path;

        pathSet.insert(beginWord);
        path.emplace_back(beginWord);
        dfs(beginWord, endWord, pathSet, path);

        return finalPath;
    }
};

```
