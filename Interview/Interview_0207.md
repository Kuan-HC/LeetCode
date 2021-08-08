# 面試金典 0207 兩個鏈表的第一個公共節點

給你兩個單鏈表的頭節點 headA 和 headB ，請你找出並返回兩個單鏈表相交的起始節點。如果兩個鏈表沒有交點，返回 null 。

[LeetCode](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/)

如下面的兩個鏈表：

<img src="img/0207.png" width = "600"/>

* 如果兩個鏈表沒有交點，返回 null.
* 在返回結果後，兩個鏈表仍須保持原有的結構。
* 可假定整個鏈表結構中沒有循環。
* 程序盡量滿足 O(n) 時間覆雜度，且僅用 O(1) 內存。

## Solution  

### C++

* 時間複雜度：O(n) n為兩個鍊的長度合

* 空間複雜度：O(1)

* 在各個鍊表的最末加上一個 nullptr

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB)
    {
        if(headA == nullptr || headB == nullptr)
            return nullptr;

        ListNode *startA = headA;
        ListNode *startB = headB;

        while (headA != headB)
        {
            if (headA == nullptr)
                headA = startB;
            else
                headA = headA->next;

            if (headB == nullptr)
                headB = startA;
            else
                headB= headB->next;
        }

        return headA;
    }
};

int main()
{
    /* input*/
    struct ListNode A(1), B(2), C(3), D(4), E(5);
    A.next = &B;
    
    C.next = &D;
    D.next = &E;

    /* Test*/
    Solution test;
    ListNode* res = test.getIntersectionNode(&A, &C);

    return 0;
}
```