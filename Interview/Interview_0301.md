# 面試金典 0301 三合一


三合一。描述如何只用一個數組來實現三個棧。

你應該實現push(stackNum, value)、pop(stackNum)、isEmpty(stackNum)、peek(stackNum)方法。stackNum表示棧下標，value表示壓入的值。

構造函數會傳入一個stackSize參數，代表每個棧的大小。

[LeetCode](https://leetcode-cn.com/problems/three-in-one-lcci/)

### example 1

```
 輸入：
["TripleInOne", "push", "push", "pop", "pop", "pop", "isEmpty"]
[[1], [0, 1], [0, 2], [0], [0], [0], [0]]
 輸出：
[null, null, null, 1, -1, -1, true]
說明：當棧為空時`pop, peek`返回-1，當棧滿時`push`不壓入元素。
```

### example 2

```
 輸入：
["TripleInOne", "push", "push", "push", "pop", "pop", "pop", "peek"]
[[2], [0, 1], [0, 2], [0, 3], [0], [0], [0], [0]]
 輸出：
[null, null, null, null, 2, 1, -1, -1]
```


## Solution  

### C++

```
#include <vector>

using namespace std;

class TripleInOne
{
private:
    vector<vector<int>> stacks;
    int size{0};

public:
    TripleInOne(int stackSize)
    {
        stacks.resize(3);
        size = stackSize;
    }

    void push(int stackNum, int value)
    {
        if (stacks[stackNum].size() < size)
            stacks[stackNum].push_back(value);
    }

    int pop(int stackNum)
    {
        if (stacks[stackNum].empty() == true)
            return -1;

        int tmp = stacks[stackNum].back();
        stacks[stackNum].pop_back();

        return tmp;
    }

    int peek(int stackNum)
    {
        if (stacks[stackNum].empty() == true)
            return -1;       

        return stacks[stackNum].back();
    }

    bool isEmpty(int stackNum)
    {
        return stacks[stackNum].empty();
    }
};

int main()
{
    /* input*/

    /* Test*/
    TripleInOne test(1);
    test.push(0, 1);
    test.push(0, 2);
    int pop_1 = test.pop(0);
    int pop_2 = test.pop(0);
    int pop_3 = test.pop(0);
    int empty = test.isEmpty(0);

    return 0;
}
```