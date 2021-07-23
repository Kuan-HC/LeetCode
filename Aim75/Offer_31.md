# 劍指 Offer 31 棧的壓入、彈出序列

輸入兩個整數序列，第一個序列表示棧的壓入順序，請判斷第二個序列是否為該棧的彈出順序。假設壓入棧的所有數字均不相等。
例如，序列 {1,2,3,4,5} 是某棧的壓棧序列，序列 {4,5,3,2,1} 是該壓棧序列對應的一個彈出序列，
但 {4,3,5,1,2} 就不可能是該壓棧序列的彈出序列。


[LeetCode](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)


### Example 1

```
輸入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
輸出：true
解釋：我们可以按以下順序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

### Example 2
```
輸入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
輸出：false
解釋：1 不能在 2 之前彈出。
```
 
## Solution  

### C++

* 時間複雜度：其中 N 為列表 pushed 的長度；每個元素最多入棧與出棧一次，即最多共 2N 次出入棧操作。


* 空間複雜度：O(n) 輔助棧 stackstack 最多同時存儲 N 個元素。

```
#include <vector>
#include <stack>

using namespace std;

class Solution
{

public:
    bool validateStackSequences(vector<int> &pushed, vector<int> &popped)
    {
        /* set dynamic programming space*/
        int len = pushed.size();
        if (len <= 2)
            return true;

        stack<int> stackInt;
        int i = 0;

        /* push num into stack untill meet the popped */
        for (const int &num : pushed)
        {
            stackInt.push(num);
            while (stackInt.empty() != true && stackInt.top() == popped[i])
            {
                stackInt.pop();
                ++i;
            }
        }

        return stackInt.empty();
    }
};

int main()
{
    /* input*/
    vector<int> pushed = {1, 2, 3, 4, 5};
    vector<int> popped = {4, 3, 5, 1, 2};

    /* Test*/
    Solution test;
    bool res = test.validateStackSequences(pushed, popped);

    return 0;
}
```

## Solution 2

* 時間複雜度：O(n) n個元素

* 空間複雜度：O(n) map及dp各需要n


```
#include <vector>
#include <unordered_map>

using namespace std;

class Solution
{

public:
    bool validateStackSequences(vector<int> &pushed, vector<int> &popped)
    {
        /* set dynamic programming space*/
        int len = pushed.size();
        if (len <= 2)
            return true;

        vector<bool> dp(len, false);
        /* initialize dp space*/
        int popId = 0;
        int i = 0;

        unordered_map<int, int> map;
        for (; i < len; ++i)
            map[pushed[i]] = i;

        dp[map[popped[popId]]] = true;
        int rLimit = map[popped[popId]];
        int ready = rLimit - 1;

        /* dynammic programming*/
        for (popId = 1; popId < len; ++popId)
        {
            int tmp_B = popped[popId];
            i = map[popped[popId]];
            if (i > rLimit)
            {
                dp[i] = true;
                rLimit = i;
                ready = rLimit - 1;
            }
            else if (i == ready)
            {
                dp[i] = true;
                ready--;
            }
            else
                return false;

            while (ready >= 0 && dp[ready] == true)
                ready--;
        }

        return true;
    }
};

int main()
{
    /* input*/
    vector<int> pushed = {2, 1, 3, 0};
    vector<int> popped = {1, 0, 3, 2};

    /* Test*/
    Solution test;
    bool res = test.validateStackSequences(pushed, popped);

    return 0;
}
```