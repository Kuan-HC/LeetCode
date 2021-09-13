# 面試金典 0502 二進制數轉字符串

二進制數轉字符串。給定一個介於0和1之間的實數（如0.72），類型為double，打印它的二進制表達式。如果該數字無法精確地用32位以內的二進制表示，則打印“ERROR”。


##  Bianry Number to String LCCI
Given a real number between 0 and 1 (e.g., 0.72) that is passed in as a double, print the binary representation. If the number cannot be represented accurately in binary with at most 32 characters, print "ERROR".

[LeetCode](https://leetcode-cn.com/problems/bianry-number-to-string-lcci)


### Example 1

```
輸入：0.625
輸出："0.101"
```

### Example 2

```
輸入：0.1
輸出："ERROR"
```

### C++ 

* 時間複雜度 O(1) 無論num為何，worst cast執行32次

* 空間複雜度 O(1)

```
class Solution {
public:
    string printBin(double num)
    {
        string ret = "0.";

        while(num != 0)
        {
            num *= 2;
            if( num >= 1){
                ret += "1";
                num -= 1;
            }
            else
            {
                ret += "0";
            }

            if(ret.size() >= 32)
                return "ERROR";
        }

        return ret;
    }
};
```
