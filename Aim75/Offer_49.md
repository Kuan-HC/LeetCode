# 劍指 Offer 49 醜數

我們把只包含質因子 2、3 和 5 的數稱作醜數（Ugly Number）。求按從小到大的順序的第 n 個醜數。

[LeetCode](https://leetcode-cn.com/problems/chou-shu-lcof/) 

### Example 1
```
輸入: n = 10
輸出: 12
解釋: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 個醜數。
```

* 1 是醜數。
* n 不超過1690。

## Solution  

### C++

* 時間複雜度：O(nlog n)。得到第 n 個醜數需要進行 n 次循環，每次循環都要從最小堆中取出 1 個元素以及向最小堆中加入最多 3 個元素，因此每次循環的時間覆雜度是 
             O(log n+log 3n)=O(log n)，總時間覆雜度是 O(nxlog n)。

* 空間複雜度：O(n)。空間覆雜度主要取決於最小堆和哈希集合的大小，最小堆和哈希集合的大小都不會超過 3n。

```
#include <queue>
#include <unordered_set>
#include <vector>

using namespace std;

class Solution
{
public:
    int nthUglyNumber(int n)
    {
        if (n <= 1)
            return n;

        priority_queue<unsigned long, vector<unsigned long>, greater<unsigned long>> smallHeap;
        unordered_set<unsigned long> numSet;
        vector<int> candidates = {2, 3, 5};

        /* set the initial condition*/
        numSet.insert(1L);
        smallHeap.push(1L);

        unsigned long tmpHeapTop = 0;
        while (n != 0)
        {
            /* pick the smallest value from the heap*/
            tmpHeapTop = smallHeap.top();
            smallHeap.pop();
            n--;

            if(n == 0)
                break;

            /* create all possible values*/
            unsigned long tmpResult = 0;
            for (const auto &candidate : candidates)
            {
                tmpResult = tmpHeapTop * candidate;
                if (numSet.find(tmpResult) == numSet.end())
                {
                    numSet.insert(tmpResult);
                    smallHeap.push(tmpResult);
                }
            }
        }

        return tmpHeapTop;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    int res = test.nthUglyNumber(1407);

    return 0;
}
```