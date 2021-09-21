# 面試金典 0808 有重覆字符串的排列組合

有重覆字符串的排列組合。編寫一種方法，計算某字符串的所有排列組合。
 
##  Permutation

Write a method to compute all permutations of a string whose characters are not necessarily unique. The list of permutations should not have duplicates.


[LeetCode](https://leetcode-cn.com/problems/permutation-ii-lcci/)


### Example 1

```
Input: S = "qqe"
Output: ["eqq","qeq","qqe"]
```

### Example 2

```
 Input: S = "ab"
 Output: ["ab", "ba"]
```

### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(n)

```
#include <string>
#include <vector>
#include <unordered_set>

using namespace std;

class Solution
{
private:
    vector<bool> used;
    unordered_set<string> set;
    vector<string> ret;
    int lenS{0};

    void dfs(const string& S, string& input)
    {
        if(input.size() == lenS){
            set.insert(input);
            return;
        }

        for(int i = 0; i < lenS; ++i)
        {
            if(used[i] != true){
                input += S[i];
                used[i] = true;
                dfs(S, input);
                used[i] = false;
                input.erase(input.end() - 1);
            }
        }
    }
public:
    vector<string> permutation(string S)
    {
        lenS = S.size();
        if(lenS == 1)
            return vector<string>{S};
        
        used.resize(lenS, false);
        string input = "";

        dfs(S, input);

        for(const string& item : set)
            ret.push_back(item);

        return ret;
    }
};
```
