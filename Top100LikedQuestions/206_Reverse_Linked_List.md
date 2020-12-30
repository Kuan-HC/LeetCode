#  Reverse Linked List
Reverse a singly linked list.

[LeetCode](https://leetcode.com/problems/reverse-linked-list/)

### Example :
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

# 反轉鍊表
反轉一個單鍊表


# Solution  
## iteration
  

## C

```
struct ListNode* reverseList(struct ListNode* head){
    if (head == NULL)
        return NULL;
        
    struct ListNode* tmp = NULL;
    struct ListNode* tmp_later = NULL;

    while(head != NULL){
        tmp_later = tmp;
        tmp = head;
        head = head->next;
        tmp->next = tmp_later;
    }

    return tmp;
}
```


