# 面試金典 1711 單詞距離

有個內含單詞的超大文本文件，給定任意兩個單詞，找出在這個文件中這兩個單詞的最短距離(相隔單詞數)。

如果尋找過程在這個文件中會重覆多次，而每次尋找的單詞不同，你能對此優化嗎?

## Find Closest

You have a large text file containing words. Given any two words, find the shortest distance (in terms of number of words) between them in the file. 
If the operation will be repeated many times for the same file (but different pairs of words), can you optimize your solution?

[LeetCode](https://leetcode-cn.com/problems/find-closest-lcci/)

### Example 1
```
Input: words = ["I","am","a","student","from","a","university","in","a","city"], word1 = "a", word2 = "student"
Output: 1
```

### C++ 

```
#include <vector>
#include <unordered_map>
#include <string>

using namespace std;

class Solution {
public:
    int findClosest(vector<string>& words, string word1, string word2)
    {
        int len = words.size();
        if(len == 0)
            return 0;

        unordered_map <string, vector<int>> wordIndex; 
        for(int i = 0; i < len; i++)
            wordIndex[words[i]].push_back(i);

        int ptr1 = 0;
        int ptr2 = 0;
        int diff = INT_MAX;
        while(ptr1 < wordIndex[word1].size() && ptr2 < wordIndex[word2].size())
        {
            int temp_diff = wordIndex[word1][ptr1] - wordIndex[word2][ptr2];
            diff = min(diff, abs(temp_diff));
            if(temp_diff > 0)
                ptr2++;
            else
                ptr1++;
        }
        return diff;
    }
};

int main()
{
    /* input */
    vector<string> words ={"I","am","a","student","from","a","university","in","a","city"};
    string word1 = "a";
    string word2 = "student";    

    /* Test */
    Solution test;
    int res = test.findClosest(words, word1, word2);

    return 0;
}
```
