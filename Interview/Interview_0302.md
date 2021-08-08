# 面試金典 0302 棧的最小值

請設計一個棧，除了常規棧支持的pop與push函數以外，還支持min函數，該函數返回棧元素中的最小值。
執行push、pop和min操作的時間覆雜度必須為O(1)。

[LeetCode](https://leetcode-cn.com/problems/min-stack-lcci/)

## Solution  

### C++

* 時間複雜度：O(n) 

* 空間複雜度：O(1)

```
#include <stack>

using namespace std;

class MinStack
{
private:
    stack<int> sequence;
    stack<int> minStack;

public:
    /** initialize your data structure here. */
    MinStack() {}

    void push(int x)
    {
        sequence.push(x);
        if (minStack.empty() == true || minStack.top() >= x)
            minStack.push(x);
        else
            minStack.push(minStack.top());        
    }

    void pop()
    {
        minStack.pop();
        sequence.pop();
    }

    int top()
    {
        return sequence.top();
    }

    int getMin()
    {
        return minStack.top();
    }
};

int main()
{
    /* input*/

    /* Test*/
    MinStack minStack;
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    int test_1 = minStack.getMin(); // 返回 -3.
    minStack.pop();
    minStack.top();                 // 返回 0.
    int test_2 = minStack.getMin(); // 返回 -2.

    return 0;
}
```