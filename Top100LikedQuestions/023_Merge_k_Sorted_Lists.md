# 023. Merge k Sorted Lists

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

[LeetCode](https://leetcode.com/problems/erge-k-sorted-lists)  

### Example 1:
```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

### Example 2:
```
Input: lists = []
Output: []
```

### Example 3:
```
Input: lists = [[]]
Output: []
```

# 合並K個升序鏈表
給你一個鏈表數組，每個鏈表都已經按升序排列。

請你將所有鏈表合並到一個升序鏈表中，返回合並後的鏈表。  

## Solution
* heap

### C++

```
#include <queue>

using namespace std;

/* Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution
{
private:
    struct smallCmp
    {
        bool operator()(const ListNode *lhs, const ListNode *rhs) const
        {
            return lhs->val > rhs->val;
        }
    };

public:
    ListNode *mergeKLists(vector<ListNode *> &lists)
    {
        int lenLists = lists.size();

        /* special cases*/
        if (lenLists == 0)
            return nullptr;
        else if (lenLists == 1)
            return lists[0];

        priority_queue<ListNode *, vector<ListNode *>, smallCmp> smallHeap;

        for (const auto &item : lists)
        {
            if (item != nullptr)
                smallHeap.push(item);
        }

        ListNode head;
        ListNode *tail = &head;

        while (smallHeap.empty() != true)
        {
            ListNode *tmp = smallHeap.top();
            smallHeap.pop();

            tail->next = tmp;

            if (tmp->next != nullptr)
                 smallHeap.push(tmp->next);

            tail = tail->next;
        }

        return head.next;
    }
};

int main()
{
    /* Input*/
    ListNode C(5),     F(4),     I(6);
    ListNode B(4, &C), E(3, &F), H(2,&I);
    ListNode A(1, &B), D(1, &E);
    vector<ListNode *> input = {&A, &D, &H};
    

    /* unit test*/
    Solution test;
    test.mergeKLists(input);

    return 0;
}
```

* Divide-and-conquer algorithm

### C++
```
struct ListNode
{
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution
{
private:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
    {
        if (l1 == nullptr || l2 == nullptr)
            return l1 == nullptr ? l2 : l1;

        if (l1->val <= l2->val)
        {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
        else
        {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }

    ListNode *split(vector<ListNode *> &lists, int lId, int rId)
    {
        if (lId == rId)
            return lists[lId];
        else if (lId > rId)
            return nullptr;

        int mid = (lId + rId) / 2;

        return mergeTwoLists(split(lists, lId, mid), split(lists, mid + 1, rId));
    }

public:
    ListNode *mergeKLists(vector<ListNode *> &lists)
    {
        int len = lists.size();

        return split(lists, 0, len - 1);
    }
};

int main()
{
    /* Input*/
    ListNode C(5), F(4), I(6);
    ListNode B(4, &C), E(3, &F), H(2, &I);
    ListNode A(1, &B), D(1, &E);
    vector<ListNode *> input = {&A, &D, &H};    

    /* unit test*/
    Solution test;
    ListNode *res = test.mergeKLists(input);

    return 0;
}
```