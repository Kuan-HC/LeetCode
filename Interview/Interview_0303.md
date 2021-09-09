# 面試金典 0303 堆盤子

堆盤子。設想有一堆盤子，堆太高可能會倒下來。因此，在現實生活中，盤子堆到一定高度時，我們就會另外堆一堆盤子。請實現數據結構SetOfStacks，模擬這種行為。SetOfStacks應該由多個棧組成，並且在前一個棧填滿時新建一個棧。此外，SetOfStacks.push()和SetOfStacks.pop()應該與普通棧的操作方法相同（也就是說，pop()返回的值，應該跟只有一個棧時的情況一樣）。 進階：實現一個popAt(int index)方法，根據指定的子棧，執行pop操作。

當某個棧為空時，應當刪除該棧。當棧中沒有元素或不存在該棧時，pop，popAt 應返回 -1.


##  Sum Lists

You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

[LeetCode](https://leetcode-cn.com/problems/stack-of-plates-lcci)

### Example 1

```
輸入：
["StackOfPlates", "push", "push", "popAt", "pop", "pop"]
[[1], [1], [2], [1], [], []]

輸出：
[null, null, null, 2, 1, -1]

```

### C++ 

```
class StackOfPlates
{
private:
    vector<stack<int>> stacks;
    int volume{0};

public:
    StackOfPlates(int cap) : volume(cap) {}

    void push(int val)
    {
        if(volume == 0)
            return;
            
        if (stacks.empty() == true || stacks.back().size() == volume)
            stacks.push_back(stack<int>());

        stacks.back().push(val);
    }

    int pop()
    {
        if (stacks.empty() == true)
            return -1;

        int ret = stacks.back().top();
        stacks.back().pop();

        if (stacks.back().empty() == true)
            stacks.erase(stacks.end());

        return ret;
    }

    int popAt(int index)
    {
        if (stacks.size() < index + 1)
            return -1;

        int ret = stacks[index].top();
        stacks[index].pop();

        if (stacks[index].empty() == true)
            stacks.erase(stacks.begin() + index);

        return ret;
    }
};
```
