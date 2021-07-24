# 劍指 Offer 38 字符串的排列

輸入一個字符串，打印出該字符串中字符的所有排列。 

你可以以任意順序返回這個字符串數組，但里面不能有重覆元素。

### Example 1

```
輸入：s = "abc"
輸出：["abc","acb","bac","bca","cab","cba"]
```

* 1 <= s 的長度 <= 8

[LeetCode](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

## Solution  

### C++

* 時間複雜度：O(n×n!)，其中 n 為給定字符串的長度。我們需要 O(nlogn) 的時間得到第一個排列，nextPermutation 函數的時間覆雜度為 O(n)，我們至多執行該函數O(n!) 次，
  因此總時間覆雜度為 O(n×n!+nlogn)=O(n×n!)。

* 空間複雜度：O(1)。注意返回值不計入空間覆雜度。

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

class Solution
{
private:
    vector<string> ret;
    int len{0};

    string nextPermutation(string &s)
    {
        int i = len - 2;
        /* locate the 1st letter to be swapped*/
        for (; i >= 0; --i)
        {
            if (s[i] < s[i + 1])
                break;
        }

        int targetId = i;
        if (targetId != -1)
        {
            char target = s[i];
            for (i = len - 1; i > targetId; --i)
            {
                if (s[i] > s[targetId])
                {
                    swap(s[targetId], s[i]);
                    break;
                }
            }
        }
        sort(s.begin() + targetId + 1, s.end());

        return s;
    }

public:
    vector<string> permutation(string s)
    {
        len = s.size();
        if (len == 1)
        {
            ret.push_back(s);
            return ret;
        }

        sort(s.begin(), s.end());
        string originS = s;
        string tmp = "";

        do
        {
             tmp = nextPermutation(s);
             ret.push_back(tmp);
        }
        while(tmp != originS);

        return ret;
    }
};

int main()
{
    /* input*/
    string input = "aab";

    /* Test*/
    Solution test;
    vector<string> res = test.permutation(input);

    return 0;
}
```