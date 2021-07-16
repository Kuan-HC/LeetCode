# 劍指 Offer 25 合併兩個排序的鍊表

輸入兩個遞增排序的鍊表，合併這兩個鍊表並使新鍊表中的節點仍然是遞增排序的。

 
[LeetCode](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)


### Example 1
```
輸入: 1->2->4, 1->3->4
輸出: 1->1->2->3->4->4
```

* 0 <= n <= 1000

## Solution  


### C++

* 時間複雜度: O(m+n) 

* 空間複雜度: O(1) 

* heap
```
#include <vector>
#include <queue>

using namespace std;

/* Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
private:
    struct smallCmp
    {
        bool operator()(ListNode *&lhs, ListNode *&rhs)
        {
            return lhs->val > rhs->val;
        }
    };

public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
    {
        if (l1 == nullptr || l2 == nullptr)
            return l1 == nullptr ? l2 : l1;

        priority_queue<ListNode *, vector<ListNode *>, smallCmp> smallHeap;

        smallHeap.emplace(l1);
        smallHeap.emplace(l2);

        ListNode head(0);
        ListNode *tail = &head;

        while (smallHeap.empty() != true)
        {
            ListNode *tmp = smallHeap.top();
            smallHeap.pop();
            if(tmp->next != nullptr)
                smallHeap.emplace(tmp->next);

            tail->next = tmp;
            tail = tail->next;
        }

        return head.next;
    }
};

int main()
{
    /* input*/
    ListNode A(1), B(3), C(5);
    A.next = &B;
    B.next = &C;
    ListNode D(2), E(4), F(6);
    D.next = &E;
    E.next = &F;

    /* Test*/
    Solution test;
    ListNode *res = test.mergeTwoLists(&A, &D);

    return 0;
}
```

* iteratioon
```
#include <vector>

using namespace std;

/* Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{

public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
    {
        ListNode head(0);
        ListNode *tail = &head;
        ListNode **tmp;

        while (l1 != nullptr && l2 != nullptr)
        {
            if (l1->val < l2->val)
                tmp = &l1;
            else
                tmp = &l2;
                
            tail->next = *tmp;
            *tmp = (*tmp)->next;

            tail = tail->next;
        }

        if (l1 == nullptr || l2 == nullptr)
            tail->next = l1 == nullptr ? l2 : l1;

        return head.next;
    }
};

int main()
{
    /* input*/
    ListNode A(1), B(3), C(5);
    A.next = &B;
    B.next = &C;
    ListNode D(2), E(4), F(6);
    D.next = &E;
    E.next = &F;

    /* Test*/
    Solution test;
    ListNode *res = test.mergeTwoLists(&A, &D);

    return 0;
}
```