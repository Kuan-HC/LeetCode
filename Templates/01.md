# KMP 算法

KMP算法核心就是維護一個next數組，不必像暴力搜索一樣，目標串每次只能往前移動一個字符，而是可以根據next的指向，移動到下一個有可能完成匹配的下標處

[CSDN](https://www.cnblogs.com/YWT-Real/p/17063212.html)

### C++ 

```
#include <vector>
#include <string>

using std::vector;
using std::string;

int kmpFind(const string &s, const string &p, int start = 0){
    int &&sLen = s.length();
    int &&pLen = p.length();

    if (pLen == 0)
        return 0;

    // 預處理字符串, next[i]代表著可以跳過匹配的數量
    vector<int> next(pLen);
    for (int i = 1, j = 0; i < pLen; ++i){
        while (j > 0 && p[i] != p[j])
            j = next[j - 1];

        if (p[i] == p[j])
            ++j;

        next[i] = j;
    }

    //匹配處理
    for (int i = start, j = 0; i < sLen; ++i){
        while (j > 0 && s[i] != p[j])
            j = next[j - 1];

        if (s[i] == p[j])
            ++j;

        if (j == pLen)
            return i - pLen + 1;
    }
    return -1;
}

int main(int argc, char **argv){
    string s = "abababcaa";
    string p = "ababc";

    auto res = kmpFind(s, p, 2);

    return 0;
}


```