# 面試金典 0507 配對交換

編寫程序，交換某個整數的奇數位和偶數位，盡量使用較少的指令（也就是說，位0與位1交換，位2與位3交換，以此類推）。

### Example 1
```
輸入：num = 2（或者0b10）
輸出 1 (或者 0b01)
```

### Example 1
```
輸入：num = 3
輸出：3
```

[LeetCode](https://leetcode-cn.com/problems/exchange-lcci/)

## Solution  

### C++

* 時間複雜度 O(1) 

* 空間複雜度 O(1) 

```
class Solution
{
public:
  int exchangeBits(int num)
  {
    /* nums range between 0 - 2^30 - 1*/

    for (int i = 0; i < 29; i+=2)
    {

      int odd = num & 1 << i;
      int even = num & (1 << (i + 1));

      num = num - odd - even + (odd << 1) + (even >> 1);
    }
    return num;
  }
};

int main()
{

  Solution test;
  int res = test.exchangeBits(3);

  return 0;
}
```