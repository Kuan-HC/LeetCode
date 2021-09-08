# 面試金典 0203 刪除中間節點

若鏈表中的某個節點，既不是鏈表頭節點，也不是鏈表尾節點，則稱其為該鏈表的「中間節點」。

假定已知鏈表的某一個中間節點，請實現一種算法，將該節點從鏈表中刪除。

例如，傳入節點 c（位於單向鏈表 a->b->c->d->e->f 中），將其刪除後，剩余鏈表為 a->b->d->e->f 


##  Delete Middle Node

Implement an algorithm to delete a node in the middle (i.e., any node but the first and last node, not necessarily the exact middle) of a singly linked list, given only access to that node.


[LeetCode](https://leetcode-cn.com/problems/delete-middle-node-lcci/)

### Example 1

```
輸入：節點 5 （位於單向鏈表 4->5->1->9 中）
輸出：不返回任何數據，從鏈表中刪除傳入的節點 5，使鏈表變為 4->1->9

```

### C++ 

* 時間複雜度 O(1)

* 空間複雜度 O(1)

```
class Solution {
public:
    void deleteNode(ListNode* node)
    {
       node->val = node->next->val;
       node->next = node->next->next;        
    }
};
```
