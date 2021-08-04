# 劍指 Offer 66 構建乘積數組

給定一個數組 A[0,1,…,n-1]，請構建一個數組 B[0,1,…,n-1]，其中 B[i] 的值是數組 A 中除了下標 i 以外的元素的積, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

[LeetCode](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

### Example 1
```
輸入: [1,2,3,4,5]
輸出: [120,60,40,30,24]
``` 

提示：

* 所有元素乘積之和不會溢出 32 位整數
* a.length <= 100000


## Solution  



### C++

* 時間複雜度：O(n) : 需遍曆兩次，O(2n)

* 空間複雜度：O(1) 使用常數大小的額外空間



```
class Solution
{
public:
    vector<int> constructArr(vector<int> &a)
    {
        int len = a.size();
        if (len <= 1)
            return a;

        /* calculate left region and temporaily stored in ret*/
        vector<int> ret(len, 1);
        int i = 1;
        for (; i < len; ++i)
            ret[i] = ret[i - 1] * a[i - 1];

        /* right region*/
        int tmp = 1;
        for (i = len - 2; i >= 0; --i)
        {
            tmp *= a[i+1];
            /* calculate left * right*/
            ret[i] *= tmp;
        }
        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> input = {1, 2, 3, 4, 5};

    /* Test*/
    Solution test;
    vector<int> res = test.constructArr(input);

    return 0;
}
```