# 面試金典 1720 連續中值

隨機產生數字並傳遞給一個方法。你能否完成這個方法，在每次產生新值時，尋找當前所有值的中間值（中位數）並保存。

中位數是有序列表中間的數。如果列表長度是偶數，中位數則是中間兩個數的平均值。

例如，

[2,3,4] 的中位數是 3

[2,3] 的中位數是 (2 + 3) / 2 = 2.5

設計一個支持以下兩種操作的數據結構：

void addNum(int num) - 從數據流中添加一個整數到數據結構中。
double findMedian() - 返回目前所有元素的中位數。


[LeetCode](https://leetcode-cn.com/problems/continuous-median-lcci/)

### Example 1
```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2

```

### C++ 

```
class MedianFinder
{
private:
    priority_queue<int, vector<int>, less<int>> smallHeap;
    priority_queue<int, vector<int>, greater<int>> bigHeap;

public:
    /** initialize your data structure here. */
    MedianFinder() {}

    void addNum(int num)
    {
        smallHeap.push(num);
        bigHeap.push(smallHeap.top());
        smallHeap.pop();

        if (bigHeap.size() > smallHeap.size())
        {
            smallHeap.push(bigHeap.top());
            bigHeap.pop();
        }
    }

    double findMedian()
    {
        if (bigHeap.size() == smallHeap.size())
            return ((double)bigHeap.top() + smallHeap.top()) / 2;

        return smallHeap.top();
    }
};
```
