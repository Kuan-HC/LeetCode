# 面試金典 0305 棧排序

棧排序。 編寫程序，對棧進行排序使最小元素位於棧頂。最多只能使用一個其他的臨時棧存放數據，但不得將元素覆制到別的數據結構（如數組）中。
該棧支持如下操作：push、pop、peek 和 isEmpty。當棧為空時，peek 返回 -1。

[LeetCode](https://leetcode-cn.com/problems/sort-of-stacks-lcci/)
示例1:

### example 1
```
輸入：
["SortedStack", "push", "push", "peek", "pop", "peek"]
[[], [1], [2], [], [], []]
輸出：
[null,null,null,1,null,2]
```

### example 2
```
輸入： 
["SortedStack", "pop", "pop", "push", "pop", "isEmpty"]
[[], [], [], [1], [], []]
輸出：
[null,null,null,null,null,true]
```


### C++

```
#include <stack>

using namespace std;

class SortedStack
{
private:
    stack<int> smallTop;
    stack<int> helper;

public:
    SortedStack()
    {
    }

    void push(int val)
    {
        while (smallTop.empty() != true && smallTop.top() < val)
        {
            helper.push(smallTop.top());
            smallTop.pop();
        }
        smallTop.push(val);

        while (helper.empty() != true)
        {
            smallTop.push(helper.top());
            helper.pop();
        }
    }

    void pop()
    {
        if (smallTop.empty() != true)
            smallTop.pop();
    }

    int peek()
    {
        return smallTop.empty() ? -1 : smallTop.top();
    }

    bool isEmpty()
    {
        return smallTop.empty();
    }
};
```