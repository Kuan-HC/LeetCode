# 劍指 OfferII 0101 判定字符是否唯一

實現一個算法，確定一個字符串 s 的所有字符是否全都不同。


[LeetCode](https://leetcode-cn.com/problems/is-unique-lcci/)

### Example 1
```
輸入: s = "leetcode"
輸出: false 
```

### Example 2
```
輸入: s = "abc"
輸出: true
```

* 0 <= len(s) <= 100
* 如果你不使用額外的數據結構，會很加分。

### C++

* 時間複雜度：o(n) 

* 空間複雜度：o(1) 

```
class Solution
{
public:
    bool isUnique(string astr)
    {
        int tmp = 0;
        int move = 0;

        for (const auto &c : astr)
        {
            
            /* use a as start point, other letter move n bit
               n = c - 'a*/
            move = c - 'a';
            tmp ^= 1 << move;
            if ((tmp & (1<< move))== 0)
                return false;
        }

        return true;
    }
};
```

### C++
* Set

* 時間複雜度：o(n log n) set插入的時間複雜度為 log n，最差情況需遍曆至字符最後一個

* 空間複雜度：o(n) set所佔空間

```
#include <string>
#include <unordered_set>

using namespace std;

class Solution
{
public:
    bool isUnique(string astr)
    {
        unordered_set<char> charSet;

        for (const auto &c : astr)
        {
            if(charSet.find(c) != charSet.end())
                return false;
            
            charSet.insert(c);
        }

        return true;
    }
};

int main()
{
    /* input*/
    string input = "leetcode";
    /* Test*/
    Solution test;
    bool res = test.isUnique(input);

    return 0;
}
```
