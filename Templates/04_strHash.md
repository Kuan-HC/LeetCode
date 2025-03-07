# 雙值哈希

雙值哈希（double hashing）是一種用於解決哈希衝突的技術，通常應用於字符串哈希中。  
其基本原理是使用兩個哈希函數來計算哈希值，以提高哈希表的性能並減少衝突。

* 模數用大質數 

constexpr ull MOD1 = 212370440130137957ll; 

constexpr ull MOD2 = 1E9 + 7; 

* 並且進制數不要選太簡單的，比如 233和 13131 這樣的，盡量大一點，比如1313131和233333 

### C++ 

```
class Solution {
public:
    int countDistinct(string s) {
        typedef unsigned long long ull;
        constexpr ull MOD1 = 212370440130137957ll;
        constexpr ull MOD2 = 1E9 + 7;
        constexpr ull BASE = 1313131;
        const int& len = s.length();

        unordered_set<ull> set1;
        unordered_set<ull> set2;
        int ret = 0;

        for(int i = 0; i < len; ++i){
            ull hash1 = 0;
            ull hash2 = 0;
            for(int j = i; j < len; ++j){                
                hash1 = hash1 * BASE + s[j];
                hash1 %= MOD1;
                hash2 = hash2 * BASE + s[j];
                hash2 %= MOD2;
                bool unique1 = set1.insert(hash1).second;
                bool unique2 = set2.insert(hash2).second;
                if(unique1 || unique2)
                    ++ret;
            }
        }

        return ret;
    }
};
```