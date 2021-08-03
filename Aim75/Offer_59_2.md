# 劍指 Offer 59-2 隊列的最大值

請定義一個隊列並實現函數 max_value 得到隊列里的最大值，要求函數max_value、push_back 和 pop_front 的均攤時間覆雜度都是O(1)。

若隊列為空，pop_front 和 max_value 需要返回 -1

[LeetCode](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

### Example 1
```
輸入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
輸出: [null,null,null,2,1,2]
```

### Example 1
```
輸入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
輸出: [null,-1,-1]
```

* 1 <= push_back,pop_front,max_value的總操作數 <= 10000
* 1 <= value <= 10^5

## Solution  

### C++

* 時間複雜度：O(1)（插入，刪除，求最大值）
            刪除操作於求最大值操作顯然只需要 O(1) 的時間。
            而插入操作雖然看起來有循環，做一個插入操作時最多可能會有 n 次出隊操作。但要注意，由於每個數字只會出隊一次，
            因此對於所有的 n 個數字的插入過程，對應的所有出隊操作也不會大於 n 次。因此將出隊的時間均攤到每個插入操作上，時間覆雜度為 O(1)。

* 空間複雜度：O(n) 需要用隊列存儲所有插入的元素

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