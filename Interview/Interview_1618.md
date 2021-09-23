# 面試金典 1618 模式匹配

你有兩個字符串，即pattern和value。 pattern字符串由字母"a"和"b"組成，用於描述字符串中的模式。
例如，字符串"catcatgocatgo"匹配模式"aabab"（其中"cat"是"a"，"go"是"b"），該字符串也匹配像"a"、"ab"和"b"這樣的模式。
但需注意"a"和"b"不能同時表示相同的字符串。編寫一個方法判斷value字符串是否匹配pattern字符串。

## Contiguous Sequence

You are given an array of integers (both positive and negative). Find the contiguous sequence with the largest sum. Return the sum.
 
[LeetCode](https://leetcode-cn.com/problems/pattern-matching-lcci/)

### Example 1
```
Input: pattern = "abba", value = "dogcatcatdog"
Output: true
```


### C++ 

```
class Solution
{
private:
    bool pass{true};
    void compareStr(string &baseStr, const string &value, bool &initialized, int &startId, const int &offset){
        if (initialized == false)
        {
            initialized = true;
            baseStr = value.substr(startId, offset);
        }
        else{
            string testStr = value.substr(startId, offset);
            if (testStr != baseStr)
                pass = false;
        }
        //startId += offset;
    }

public:
    bool patternMatching(string pattern, string value){
        int strLen = value.size();
        if (pattern.size() == 1)
            return true;

        /* 統計 a及b的個數*/
        int amountA = 0;
        int amountB = 0;
        for (const char &c : pattern){
            if (c == 'a')
                amountA++;
            else
                amountB++;
        }

        /* 若只有單一原素*/
        string baseStrA = "";
        bool initializedA = false;
        pass = true;
        if (amountA == 0 || amountB == 0){
            int items = amountA == 0 ? amountB : amountA;
            if (strLen % items != 0)
                return false;
            int itemLen = strLen / items;

            for (int start = 0; start < strLen; start += itemLen){
                compareStr(baseStrA, value, initializedA, start, itemLen);
                if (pass == false)
                    return false;
            }
            return true;
        }

        /* 由 a 的長度 0 開始，一直到 b的長度為0*/
        string baseStrB = "";
        bool initializedB = false;

        for (int aLen = 0; aLen * amountA <= strLen; aLen++){
            pass = true;
            initializedA = false;
            initializedB = false;
            baseStrB = "";

            int start = 0; // 由start位置開始截取 字符
            if ((strLen - aLen * amountA) % amountB != 0){
                pass = false;
                continue;
            }
            int bLen = (strLen - aLen * amountA) / amountB;

            for (const char &c : pattern){
                if (c == 'a'){
                    compareStr(baseStrA, value, initializedA, start, aLen);
                    if (pass == false)
                        break;

                    start += aLen;
                }
                else{
                    compareStr(baseStrB, value, initializedB, start, bLen);
                    if (pass == false)
                        break;

                    start += bLen;
                }
            }
            if (pass == true && baseStrA != baseStrB)
                return true;
        }
        return false;
    }
};

int main(void)
{
    /* input*/
    string pattern = "bbbaa";
    string value = "xxxxxxy";
    /* test*/
    Solution test;
    bool res = test.patternMatching(pattern, value);

    return 0;
}

```
