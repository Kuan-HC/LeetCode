# 面試金典 0208 環路檢測

給定一個鏈表，如果它是有環鏈表，實現一個算法返回環路的開頭節點。

[LeetCode](https://leetcode-cn.com/problems/linked-list-cycle-lcci/)

### example 1

<img src="img/0208.png" width = "600"/>


```
輸入：head = [3,2,0,-4], pos = 1
輸出：tail connects to node index 1
解釋：鍊表中有一个環，其尾部連接到第二個節點。

```

## Solution  

### C++

* 時間複雜度：O(n) 

* 空間複雜度：O(1)

```
/*  Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
public:
    ListNode *detectCycle(ListNode *head)
    {
        if (head == nullptr)
            return nullptr;

        /* set two pointer slow and fast*/
        ListNode *fast = head;
        ListNode *slow = head;

        do
        {
            if (fast->next == nullptr)
                return nullptr;

            fast = fast->next->next;
            slow = slow->next;
        } while (fast != nullptr && fast != slow);

        if (fast == nullptr)
            return nullptr;

        ListNode *third = head;
        while (third != slow)
        {
            third = third->next;
            slow = slow->next;
        }

        return third;
    }
};

int main()
{
    /* input*/
    struct ListNode A(1), B(2), C(3), D(4), E(5);
    A.next = &B;
    B.next = &C;
    C.next = &D;
    //D.next = &E;
    //E.next = &C;

    /* Test*/
    Solution test;
    ListNode *res = test.detectCycle(&A);

    return 0;
}
```