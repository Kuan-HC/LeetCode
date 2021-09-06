# 面試金典 0504 下一個數

下一個數。給定一個正整數，找出與其二進制表達式中1的個數相同且大小最接近的那兩個數（一個略大，一個略小）

### Example 1
```
輸入：num = 2（或者0b10）
輸出：[4, 1] 或者（[0b100, 0b1]）
```

### Example 1
```
輸入：num = 1
輸出：[2, -1]
```

[LeetCode](https://leetcode-cn.com/problems/closed-number-lcci/)

## Solution  

### C++

* 時間複雜度 O(1) 

* 空間複雜度 O(1) 

```
#include <bitset>
#include <vector>
#include <cmath>

using namespace std;

class Solution
{
public:
    vector<int> findClosedNumbers(int num)
    {

        vector<int> ret(2, -1);

        bitset<31> bitToGreat(num);
        bitset<31> bitToSmall(num);

        /* find the first 1 0 combination */
        int i = 0;
        for (; i < 30; i++)
        {
            if (ret[0] == -1 && bitToGreat.test(i + 1) == false && bitToGreat.test(i) == true)
            {
                bitToGreat.flip(i + 1);
                bitToGreat.flip(i);

                int count = 0;

                for (int j = 0; j < i; j++)
                {
                    if (bitToGreat.test(j) == true)
                    {
                        count++;
                        bitToGreat.reset(j);
                    }
                }
                i = 0;
                while (count > 0)
                {
                    count--;
                    bitToGreat.set(i++);
                }
                ret[0] = (int)bitToGreat.to_ulong();
            }

            if (ret[1] == -1 && bitToSmall.test(i + 1) == true && bitToSmall.test(i) == false)
            {
                bitToSmall.flip(i + 1);
                bitToSmall.flip(i);

                int count = 0;

                for (int j = 0; j < i; j++)
                {
                    if (bitToSmall.test(j) == true)
                    {
                        count++;
                        bitToSmall.reset(j);
                    }
                }

                while (count > 0)
                {
                    count--;
                    bitToSmall.set(--i);
                }
                ret[1] = (int)bitToSmall.to_ulong();
            }
        }

        return ret;
    }
};

int main()
{
    Solution test;
    vector<int> ret = test.findClosedNumbers(2);

    return 0;
}
```