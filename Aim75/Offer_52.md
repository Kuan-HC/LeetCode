# 劍指 Offer 52 兩個鏈表的第一個公共節點

輸入兩個鏈表，找出它們的第一個公共節點。

[LeetCode](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

如下面的兩個鏈表：

<img src="img/52.png" width = "600"/>

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
        if (headA == nullptr || headB == nullptr)
            return nullptr;

        /* set two pointers start from each branch*/
        ListNode *branchA = headA;
        ListNode *branchB = headB;

        while (headA != headB)
        {
            if (headA == nullptr)
                headA = branchB;
            else
                headA = headA->next;

            if (headB == nullptr)
                headB = branchA;
            else
                headB = headB->next;
        }
        return headA;
    }
};

int main()
{
    /* input*/
    ListNode A(1), B(2), C(3), D(4), E(5);
    A.next = &C;    
    B.next = &C;
    C.next = &D;
    D.next = &E;
    /* Test*/
    Solution test;
    ListNode *res = test.getIntersectionNode(&B, &A);

    return 0;
}
```