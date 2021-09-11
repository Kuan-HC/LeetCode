# 面試金典 0809 括號

括號。設計一種算法，打印n對括號的所有合法的（例如，開閉一一對應）組合。

說明：解集不能包含重覆的子集。

例如，給出 n = 3，生成結果為：

##  Bracket
Implement an algorithm to print all valid (e.g., properly opened and closed) combinations of n pairs of parentheses.

Note: The result set should not contain duplicated subsets.

For example, given n = 3, the result should be:


[LeetCode](https://leetcode-cn.com/problems/bracket-lcci)


### Example 1
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(n)

```
class Solution
{
private:
    vector<string> ret;
    void dfs(string input, int leftNum, int rightNum)
    {
        if(leftNum == 0)
        {
            while(rightNum--)
                input += ")";
            ret.push_back(input);
            return;
        }

        /* two rules:
           1. when left == right, only add left 
           2. when left == 0, right goes all the way to the end
        */

        /* add left bracket*/
        dfs(input + "(", leftNum - 1, rightNum);
        /* add right bracket*/
        if (leftNum != rightNum )
            dfs(input + ")", leftNum, rightNum - 1);       
        
    }

public:
    vector<string> generateParenthesis(int n)
    {
        string start = "(";
        dfs(start, n - 1, n);

        return ret;
    }
};
```
