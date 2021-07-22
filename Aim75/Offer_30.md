# 劍指 Offer 30 包含min函数的棧

定義棧的數據結構，請在該類型中實現一個能夠得到棧的最小元素的 min 函數在該棧中，調用 min、push 及 pop 的時間覆雜度都是 O(1)。

[LeetCode](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

### Example 1

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.

```


* 各函數的調用總次數不超過 20000 次

 
## Solution  

### C++

* 時間複雜度 O(1) ： push(), pop(), top(), min() 四個函數的時間覆雜度均為常數級別。

* 空間複雜度 O(N) ： 當共有 N 個待入棧元素時，輔助棧 BB 最差情況下存儲 N 個元素，使用 O(N) 額外空間。

<img src="img/30.gif" width = "500"/>

[LeetCode Solution](https://leetcode-cn.com/problems/min-stack/solution/zui-xiao-zhan-by-leetcode-solution/)

```
#include <stack>
#include <vector>

using namespace std;

class MinStack
{
private:
    stack<int> intStack;
    stack<int> minStack;

public:
    /** initialize your data structure here. */
    MinStack() {}

    void push(int x)
    {
        intStack.push(x);
        if (minStack.empty() == true || x < minStack.top())
            minStack.push(x);
        else
            minStack.push(minStack.top());
    }

    void pop()
    {
        intStack.pop();
        minStack.pop();
    }

    int top()
    {
        return intStack.top();
    }

    int min()
    {
        return minStack.top();
    }
};

int main()
{
    /* input*/

    /* Test*/
    int min;
    int top;

    MinStack *obj = new MinStack(); //n
    obj->push(-10);                 //n
    obj->push(14);                  //n
    min = obj->min();               //-10
    min = obj->min();               // -10
    obj->push(-20);                 // n
    min = obj->min();               // -20
    min = obj->min();               //-20
    top = obj->top();               //-20
    min = obj->min();               //-20
    obj->pop();                     //n
    obj->push(10);                  //n
    obj->push(-7);                  //n
    min = obj->min();               //-10
    obj->push(-7);                  //n
    obj->pop();                     //n
    top = obj->top();               //-7
    min = obj->min();               //-10
    obj->pop();                     //null

    return 0;
}
```