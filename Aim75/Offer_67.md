# 劍指 Offer 66 把字符串轉換成整數

首先，該函數會根據需要丟棄無用的開頭空格字符，直到尋找到第一個非空格的字符為止。

當我們尋找到的第一個非空字符為正或者負號時，則將該符號與之後面盡可能多的連續數字組合起來，作為該整數的正負號；假如第一個非空字符是數字，則直接將其與之後連續的數字字符組合起來，形成整數。

該字符串除了有效的整數部分之後也可能會存在多余的字符，這些字符可以被忽略，它們對於函數不應該造成影響。

注意：假如該字符串中的第一個非空格字符不是一個有效整數字符、字符串為空或字符串僅包含空白字符時，則你的函數不需要進行轉換。

在任何情況下，若函數不能進行有效的轉換時，請返回 0。

[LeetCode](https://leetcode-cn.com/problems/)

假設我們的環境只能存儲 32 位大小的有符號整數，那麽其數值範圍為 [−231,  231 − 1]。如果數值超過這個範圍，請返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

### Example 1
```
輸入: "42"
輸出: 42
```

### Example 2
```
輸入: "   -42"
輸出: -42
解釋: 第一個非空白字符為 '-', 它是一個負號。
     我們盡可能將負號與後面所有連續出現的數字組合起來，最後得到 -42 。
```

### Example 3
```
輸入: "4193 with words"
輸出: 4193
解釋: 轉換截止於數字 '3' ，因為它的下一個字符不為數字。
```

### Example 4
```
輸入: "words and 987"
輸出: 0
解釋: 第一個非空字符是 'w', 但它不是數字或正、負號。
     因此無法執行有效的轉換。
```

### Example 5
```
輸入: "-91283472332"
輸出: -2147483648
解釋: 數字 "-91283472332" 超過 32 位有符號整數範圍。 
     因此返回 INT_MIN (−231) 。
```

## Solution  

### C++

* 時間複雜度：O(n) : 需遍曆所有的字母

* 空間複雜度：O(1) 使用常數大小的額外空間

```
#include <string>

using namespace std;

class Solution
{
private:
    enum processState
    {
        ready,
        posNeg,
        valProcess,
        end
    };

public:
    int strToInt(string str)
    {
        unsigned int value = 0;
        bool neg = false;

        processState state = ready;

        for (const auto &c : str)
        {
            switch (state)
            {
            case ready:
                /* code */
                if (c == ' ')
                    state = ready;
                else if (c == '+' || c == '-')
                    state = posNeg;
                else if (c < 48 || c > 57)
                    state = end;
                else
                    state = valProcess;
                break;

            case posNeg:
                if (c < 48 || c > 57)
                    state = end;
                else
                    state = valProcess;
                break;

            case valProcess:
                if (c < 48 || c > 57)
                    state = end;
                break;
            }

            switch (state)
            {
            case posNeg:
                if (c == '-')
                    neg = true;
                break;

            case valProcess:
                if ((value == INT_MAX / 10 && c > '7') || value > INT_MAX / 10)
                {
                    if (neg)
                        return INT_MIN;
                    return INT_MAX;
                }
                value = value * 10 + (c - '0');
                break;
            }
        }
        if(neg)
            value *= -1;

        return value;
    }
};

int main()
{
    /* input*/
    string input = "  -42";
    /* Test*/
    Solution test;
    int res = test.strToInt(input);

    return 0;
}
```