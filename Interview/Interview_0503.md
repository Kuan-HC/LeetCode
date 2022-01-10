# 面試金典 0503 翻轉數位

給定一個32位整數 num，你可以將一個數位從0變為1。請編寫一個程序，找出你能夠獲得的最長的一串1的長度。
 
##  Reverse Bits

You have an integer and you can flip exactly one bit from a 0 to a 1. Write code to find the length of the longest sequence of 1s you could create.

[LeetCode](https://leetcode-cn.com/problems/reverse-bits-lcci)


### Example 1

```
Input: num = 1775(11011101111)
Output: 8
```

### Example 2

```
Input: num = 7(0111)
Output: 4
```

### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(1)

```
#include <bitset>

using namespace std;

/* * Definition for a binary tree node. */
class Solution
{
public:
    int reverseBits(int num)
    {
        if (num == -1)
            return 32;
            
        bitset<32> numBit(num);
        /* iterate each bit, if that bit is 0, expand from it */
        int left = 0;
        int right = 0;
        int maxLength = 0;
        for (int i = 0; i < 32; ++i)
        {
            if (numBit.test(i) == false)
            {
                left = i;
                right = i;
                while (left - 1 >= 0 && numBit.test(left - 1) == true)
                    left--;
                while (right + 1 < 32 && numBit.test(right + 1) == true)
                    right++;

                maxLength = max(maxLength, right - left + 1);
            }
        }
        return maxLength;
    }
};

int main()
{
    /* input */

    /* test*/
    Solution test;
    int res = test.reverseBits(-1);

    return 0;
}
```
