# 面試金典 0202 返回倒數第K個節點

實現一種算法，找出單向鏈表中倒數第 k 個節點。返回該節點的值。

## Kth Node From End of List 

Implement an algorithm to find the kth to last element of a singly linked list. Return the value of the element.
 
[LeetCode](https://leetcode-cn.com/problems/kth-node-from-end-of-list-lcci/)

### Example 1
```
Input:  1->2->3->4->5 和 k = 2
Output:  4
```

### C++ 

* 空間複雜度 O(n)

* 時間複雜度 O(1)

```
class Solution {
public:
    int kthToLast(ListNode* head, int k) {
        ListNode* second = head;

        while( head != nullptr)
        {
            head = head->next;
            if( k > 0)
                k--;
            else
                second = second->next;
        }
        return second->val;
    }
};
```
