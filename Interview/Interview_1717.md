# 面試金典 1717 多次搜索

給定一個較長字符串big和一個包含較短字符串的數組smalls，設計一個方法，根據smalls中的每一個較短字符串，對big進行搜索。輸出smalls中的字符串在big里出現的所有位置positions，其中positions[i]為smalls[i]出現的所有位置。

## Multi Search

Given a string band an array of smaller strings T, design a method to search b for each small string in T. Output positions of all strings in smalls that appear in big, where positions[i] is all positions of smalls[i].

[LeetCode](https://leetcode-cn.com/problems/multi-search-lcci/)

### Example 1
```
Input: 
big = "mississippi"
smalls = ["is","ppi","hi","sis","i","ssippi"]
Output:  [[1,4],[8],[],[3],[1,4,7,10],[5]]

```

### C++ 

```
class Trie
{
    public:
    bool isEnd{false};
    int id{0};
    Trie* next[26]{nullptr};

    void insert(string word, int smallsId)
    {
        Trie* currPos = this;
        int num = 0;
        for(const char& c: word)
        {
            num = c - 'a';
            if(currPos->next[num] == nullptr)
                currPos->next[num] = new Trie();
            
            currPos = currPos->next[num];
        }
        currPos->isEnd = true;
        currPos->id = smallsId;
    }
};
class Solution
{
public:
    vector<vector<int>> multiSearch(string big, vector<string> &smalls)
    {
        int lenSmall = smalls.size();
        int lenBig = big.length();
        if(lenSmall == 0)
            return {{}};
        
        vector<vector<int>> ret(lenSmall, vector<int>(0));
        if(lenBig == 0)
            return ret;

        Trie* dictTree = new Trie();

        for(int i = 0; i < lenSmall; ++i)
            dictTree->insert(smalls[i], i);

        int num = 0;
        for(int i = 0; i < lenBig; i++)
        {
            Trie* root = dictTree;
            for(int j = i; j < lenBig; j++)
            {
                num = big[j] - 'a';
                if(root->next[num] == nullptr)
                    break;
                if(root->next[num]->isEnd == true)
                    ret[root->next[num]->id].push_back(i);
                root = root->next[num];
            }
        }

        return ret;
    }
};

int main(void)
{
    /* input*/
    string big = "mississippi";
    vector<string> smalls = {"is", "ppi", "hi", "sis", "i", "ssippi"};

    Solution test;
    vector<vector<int>> res = test.multiSearch(big, smalls);

    return 0;
}
```
