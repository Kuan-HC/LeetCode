# 劍指 Offer 59-1 滑動窗口的最大值

給定一個數組 nums 和滑動窗口的大小 k，請找出所有滑動窗口里的最大值。

[LeetCode](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

### Example 1
```
輸入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
輸出: [3,3,5,5,6,7] 
解釋: 

  滑動窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

* 你可以假設 k 總是有效的，在輸入數組不為空的情況下，1 ≤ k ≤ 輸入數組的大小。


## Solution  

### C++

* 時間複雜度：O(n log n)，其中 n 是數組 nums 的長度。在最壞情況下，數組 nums 中的元素單調遞增，那麽最終優先隊列中包含了所有元素，
             沒有元素被移除。由於將一個元素放入優先隊列的時間覆雜度為 O(log n)，因此總時間覆雜度為 O(n log n)。

* 空間複雜度：O(n)，即為優先隊列需要使用的空間。這里所有的空間覆雜度分析都不考慮返回的答案需要的 O(n) 空間，只計算額外的空間使用。

```
#include <deque>
#include <queue>

using namespace std;

class MaxQueue
{
private:
    deque<int> max;
    queue<int> list;

public:
    MaxQueue() {}

    int max_value()
    {
        return max.empty() ? -1 : max.front();
    }

    void push_back(int value)
    {
        list.push(value);

        if (max.empty() == true || max.back() > value)
            max.push_back(value);
        else
        {            
            while (max.empty() != true && max.back() < value)
            {    max.pop_back();}

            max.push_back(value);               
        }
    }

    int pop_front()
    {
        if (list.empty() == true)
            return -1;
        
        int ret = list.front();
        list.pop();
        if(ret == max.front())
            max.pop_front();

        return ret;
    }
};

int main()
{
    /* input*/

    /* Test*/

    MaxQueue test;
    
    test.max_value();    //-1
    test.pop_front();    //-1
    test.max_value();    //-1
    test.push_back(46);  //null
    test.max_value();    //46
    test.pop_front();    //46

    return 0;
}
```