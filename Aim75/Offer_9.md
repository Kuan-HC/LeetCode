# 劍指 Offer 09. 用兩個棧實現隊列
用兩個棧實現一個隊列。隊列的聲明如下，請實現它的兩個函數 appendTail 和 deleteHead ，分別完成在隊列尾部插入整數和在隊列頭部刪除整數的功能。
(若隊列中沒有元素，deleteHead 操作返回 -1 )

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

[LeetCode](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof)

## Solution  
* stack

<img src="img/739.gif" width = "800"/>

### C++

```
#include <stack>

using namespace std;

class CQueue
{
private:
    stack<int> output;
    stack<int> add;

public:
    CQueue(){};

    void appendTail(int value)
    {
        int tmp = 0;
        while (output.empty() != true)
        {
            tmp = output.top();
            output.pop();
            add.push(tmp);
        }

        output.push(value);

        while (add.empty() != true)
        {
            tmp = add.top();
            add.pop();
            output.push(tmp);
        }
    }

    int deleteHead()
    {
        if (output.empty() == true)
            return -1;
        
        int tmp = 0;
        tmp = output.top();
        output.pop();

        return tmp;
    }
};


int main()
{
    /**
     * Your CQueue object will be instantiated and called as such:
     */
    CQueue *obj = new CQueue();
    int a = obj->deleteHead();
    obj->appendTail(5);
    obj->appendTail(2);
    int b = obj->deleteHead();
    int c = obj->deleteHead();

    return 0;
}
```