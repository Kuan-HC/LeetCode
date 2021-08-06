# 面試金典 0102 判定是否互為字符重排

給定兩個字符串 s1 和 s2，請編寫一個程序，確定其中一個字符串的字符重新排列後，能否變成另一個字符串。

[LeetCode](https://leetcode-cn.com/problems/check-permutation-lcci/)

### Example 1
```
輸入: s1 = "abc", s2 = "bca"
輸出: true 
```

### Example 2
```
輸入: s1 = "abc", s2 = "bad"
輸出: false
```

* 0 <= len(s1) <= 100
* 0 <= len(s2) <= 100

來源：力扣（LeetCode）
鏈接：https://leetcode-cn.com/problems/check-permutation-lcci
著作權歸領扣網絡所有。商業轉載請聯系官方授權，非商業轉載請注明出處。


### C++

* 時間複雜度：o(n log n) 排序的時間複雜度

* 空間複雜度：o(1) 

```
#include <string>
#include <algorithm>

using namespace std;

class Solution
{
public:
    bool CheckPermutation(string s1, string s2)
    {
        if(s1.size() != s2.size())
            return false;
            
        sort(s1.begin(), s1.end());

        sort(s2.begin(), s2.end());

        return s1 == s2;;
    }
};

int main()
{
    /* input*/
    string input1 = "bb";
    string input2 = "bb";
    /* Test*/
    Solution test;
    bool res = test.CheckPermutation(input1, input2);

    return 0;
}
```
