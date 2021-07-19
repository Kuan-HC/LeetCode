# 劍指 Offer 16 打印從1到最大的n位數

輸入數字 n，按順序打印出從 1 到最大的 n 位十進制數。比如輸入 3，則打印出 1、2、3 一直到最大的 3 位數 999。

 
[LeetCode](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)


### Example 1

```
輸入: n = 1
輸出: [1,2,3,4,5,6,7,8,9]
```

## Solution  


### C++

* 時間複雜度：O(10^n)生成長度为 10^n 的列表需使用 O(10^n)時間。

* 空間複雜度：O(1) 建立列表需使用 O(1) 大小的額外空间（ 列表作为返回结果，不計入額外空間 ）。



```
#include <vector>

using namespace std;

class Solution {
public:
    vector<int> printNumbers(int n)
    {
        int max = 1;
        while(n-- != 0)
            max*=10;

        vector<int> ret;
        int tmp = 1;
        while(tmp != max)
            ret.push_back(tmp++);

        return ret;

    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    vector<int> res = test.printNumbers(2);

    return 0;
}
```