# 劍指 Offer 58-2 左旋轉字符串

字符串的左旋轉操作是把字符串前面的若幹個字符轉移到字符串的尾部。請定義一個函數實現字符串左旋轉操作的功能。比如，輸入字符串"abcdefg"和數字2，該函數將返回左旋轉兩位得到的結果"cdefgab"。

[LeetCode](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

### Example 1
```
輸入: s = "abcdefg", k = 2
輸出: "cdefgab"
```


### Example 2
```
輸入: s = "lrloseumgh", k = 6
輸出: "umghlrlose"
 ```

* 1 <= k < s.length <= 10000


## Solution  

### C++

* 時間複雜度：O(1) 

* 空間複雜度：O(1) 

```
#include <string>

using namespace std;

class Solution
{
public:
    string reverseLeftWords(string s, int n)
    {
        int len = s.size();
        
        if(len == 1)
            return s;

        string ret = s.substr(n, len - n );
        ret += s.substr(0, n);


        return ret;
    }
};

int main()
{
    /* input*/
    string s = "lrloseumgh";

    /* Test*/
    Solution test;
    string res = test.reverseLeftWords(s, 6);

    return 0;
}
```
### C++

```
#include <string>

using namespace std;

class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(), s.begin() + n);
        reverse(s.begin() + n, s.end());
        reverse(s.begin(), s.end());
        return s;
    }
};
```