# 面試金典 0104 回文排列

給定一個字符串，編寫一個函數判定其是否為某個回文串的排列之一。

回文串是指正反兩個方向都一樣的單詞或短語。排列是指字母的重新排列。

回文串不一定是字典當中的單詞。

 
## Palindrome Permutation

Given a string, write a function to check if it is a permutation of a palindrome. A palindrome is a word or phrase that is the same forwards and backwards. 
A permutation is a rearrangement of letters. The palindrome does not need to be limited to just dictionary words.




[LeetCode](https://leetcode-cn.com/problems/palindrome-permutation-lcci/)

### Example 1

```
輸入："tactcoa"
輸出：true（排列有"tacocat"、"atcocta"，等等）

```

### C++ 

* 時間複雜度 O(n)
* 空間複雜度 O(1)
```
class Solution
{
public:
    bool canPermutePalindrome(string s)
    {
        /* assume lowercast letter*/
        int len = s.size();

        bool odd = len & 1;

        bitset<128> map(0);

        for(const char& c : s)
            map.flip(c);


        if(odd == false && map.count() == 0)
            return true;
        
        if( odd == true && map.count() == 1)
            return true;      

        return false;
    }
};

int main()
{
    string input = "aabbcd";

    /* unit test*/
    Solution test;
    bool ret = test.canPermutePalindrome(input);

    return 0;
}
```
