# 142. Linked List Cycle II
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Notice that you should not modify the linked list.

[LeetCode](https://leetcode.com/problems/linked-list-cycle-ii)  

### Example 1:
<img src="img/142_q1.png" width = "400"/>

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

### Example 2:
```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

### Example 3:
```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

# 環形鍊表 II

為了表示給定鏈表中的環，我們使用整數 pos 來表示鏈表尾連接到鏈表中的位置（索引從 0 開始）。 如果 pos 是 -1，則在該鏈表中沒有環。
注意，pos 僅僅是用於標識環的情況，並不會作為參數傳遞到函數中。

說明：不允許修改給定的鏈表。

進階：

你是否可以使用 O(1) 空間解決此題？

## Solution

### C

* Fast and slow pointers
<img src="img/141.jpg" width = "947"/>

```
struct ListNode
{
    int val;
    struct ListNode *next;
};

struct ListNode *detectCycle(struct ListNode *head)
{
    if (head == NULL)
        return NULL;
    /**
     *  two pointers: one first and one slow
     *  when fast and slow points meet in the loop
     *  set the third pointer, it will meet the slow one
     * at the intersection
     *  */
    struct ListNode *slow = head;
    struct ListNode *fast = head;
    struct ListNode *last = head;

    /* if the cahin is not a loop, fast pointer will reach tne end*/
    while (fast != NULL)
    {
        if (fast->next != NULL)
            fast = fast->next->next;
        else
            return NULL;

        slow = slow->next;

        if (fast == slow)
        {
            while (slow != last)
            {
                slow = slow->next;
                last = last->next;
            }
            return last;
        }
    }

    return NULL;
}

int main()
{
    /* input */
    struct ListNode A, B, C, D, E;
    A.val = 3;
    A.next = &B;
    B.val = 2;
    B.next = &C;
    C.val = 0;
    C.next = &D;
    D.val = -4;
    D.next = &B;

    /* Algorithm */

    struct ListNode *ans = detectCycle(&A);

    return 0;
}
```

### C++
*Hash Table

```
#include <unordered_set>

using std::unordered_set;

/**
 * Definition for singly-linked list.
 * */

struct ListNode
{
    int val;
    struct ListNode *next;
};

class Solution
{
public:
    ListNode *detectCycle(ListNode *head)
    {
        unordered_set<ListNode *> visited;

        while (head != nullptr)
        {
            if (visited.count(head) != true)
            {
                visited.insert(head);
                head = head->next;
            }
            else
                return head;
        }

        return nullptr;
    }
};

int main()
{
    /* input */
    struct ListNode A, B, C, D, E;
    A.val = 3;
    A.next = &B;
    B.val = 2;
    B.next = &C;
    C.val = 0;
    C.next = &D;
    D.val = -4;
    D.next = &B;

    /* Algorithm */
    Solution test;
    ListNode *ans = test.detectCycle(&A);

    return 0;
}
```


