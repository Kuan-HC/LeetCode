# 劍指 Offer 50 第一個只出現一次的字符

在字符串 s 中找出第一個只出現一次的字符。如果沒有，返回一個單空格。 s 只包含小寫字母。

[LeetCode](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

### Example 1

```
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
```

* 0 <= s 的長度 <= 50000


## Solution  

### C++

* 時間複雜度：O(n)，其中 n 是字符串 s 的長度。我們需要進行兩次遍歷。

* 空間複雜度：O(∣Σ∣)，其中 Σ 是字符集，在本題中 s 只包含小寫字母，因此 ∣Σ∣≤26。我們需要 O(∣Σ∣) 的空間存儲哈希映射。


```
#include <unordered_map>
#include <string>

using namespace std;

class Solution
{
public:
    char firstUniqChar(string s)
    {
        char ret = ' ';
        if (s.size() == 0)
            return ret;

        unordered_map<char, int> map;
        for (const auto &c : s)
            map[c]++;

        for (const auto &c : s)
        {
            if (map[c] == 1)
            {
                ret = c;
                break;
            }
        }
        return ret;
    }
};

int main()
{
    /* input*/
    string input = "abaccdeff";

    /* Test*/
    Solution test;
    char res = test.firstUniqChar(input);

    return 0;
}
```