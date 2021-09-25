# 面試金典 0204 分割鍊表

給你一個鏈表的頭節點 head 和一個特定值 x ，請你對鏈表進行分隔，使得所有 小於 x 的節點都出現在 大於或等於 x 的節點之前。

你不需要 保留 每個分區中各節點的初始相對位置。

## Partition List

Write code to partition a linked list around a value x, such that all nodes less than x come before all nodes greater than or equal to x. If x is contained within the list, the values of x only need to be after the elements less than x (see below). The partition element x can appear anywhere in the "right partition"; it does not need to appear between the left and right partitions.

 
[LeetCode](https://leetcode-cn.com/problems/partition-list-lcci/)

### Example 1
```
Input: head = 3->5->8->5->10->2->1, x = 5
Output: 3->1->2->10->5->5->8
```

### C++ 

* 空間複雜度 O(n)

* 時間複雜度 O(1)

```
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {

        ListNode firstHead(-1);
        ListNode* firstTail = &firstHead;
        ListNode secondHead(-1);
        ListNode* secondTail = &secondHead;

        ListNode* temp = nullptr;
        while(head != nullptr)
        {
            temp = head;
            head = head->next;
            if(temp->val < x)
            {
                firstTail->next = temp;
                firstTail = firstTail->next;
            }
            else
            {
                secondTail->next = temp;
                secondTail = secondTail->next;
            }
        }
        secondTail->next = nullptr;
        firstTail->next = secondHead.next;

        return firstHead.next;
    }
};
```
