# 面試金典 0103 URL化

URL化。編寫一種方法，將字符串中的空格全部替換為%20。假定該字符串尾部有足夠的空間存放新增字符，並且知道字符串的“真實”長度。（注：用Java實現的話，請使用字符數組實現，以便直接在數組上操作。）

[LeetCode](https://leetcode-cn.com/problems/string-to-url-lcci/)

### Example 1
```
輸入："Mr John Smith    ", 13
輸出："Mr%20John%20Smith"
```

### Example 2
```
輸入："               ", 5
輸出："%20%20%20%20%20"
``` 

* 字符串長度在 [0, 500000] 範圍內。


### C++

* 時間複雜度：o(n) string的長度

* 空間複雜度：o(n) string的長度

```
class Solution
{
public:
    string replaceSpaces(string S, int length)
    {
        if (length == 0)
            return S;

        string ret;
        for (int i = 0; i < length; ++i)
        {
            if(S.at(i) != ' ')
                ret += S.at(i);
            else
                ret += "%20";
        }

        return ret;
    }
};



int main()
{
    /* input*/
    string input = "     ";

    /* Test*/
    Solution test;
    string res = test.replaceSpaces(input, 5);

    return 0;
}
```
