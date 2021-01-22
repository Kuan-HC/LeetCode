# 234. Palindrome Linked List
Given a singly linked list, determine if it is a palindrome.

[LeetCode](https://leetcode.com/problems/palindrome-linked-list/)

### Example 1:
```
 Input: 1->2
Output: false
```
### Example 2:
```
 Input: 1->2->2->1
Output: true
```
#  回文鍊表
請判斷一個鍊表是否為回文鍊表


## Solution  
### Make a new list, do not change the original sequence

### C

```
bool isPalindrome(struct ListNode *head)
{
    if (head == NULL || head->next == NULL)
        return true;
    /* create fast and slow pointer, fast moves two times distance as slow does*/
    //struct ListNode *fast = head;
    struct ListNode *slow = head;

    struct ListNode *copy_head = (struct ListNode *)malloc(sizeof(struct ListNode));
    copy_head->val = head->val;
    copy_head->next = NULL;
    struct ListNode *copy_tmp = copy_head;

    bool ret = true;
    while (head->next != NULL)
    {
        head = head->next;
        if (head->next != NULL)
        {
            head = head->next;
            slow = slow->next;
            copy_head = (struct ListNode *)malloc(sizeof(struct ListNode));
            copy_head->val = slow->val;
            copy_head->next = copy_tmp;
            copy_tmp = copy_head;
        }
        else
        {
            slow = slow->next;
            break;
        }
    }

    while (slow != NULL)
    {
        if (slow->val != copy_head->val)
        {
            ret = false;
            break;
        }
        slow = slow->next;
        copy_head = copy_head->next;
    }

    while (copy_tmp != NULL)
    {
        copy_head = copy_tmp->next;
        free(copy_tmp);
        copy_tmp = copy_head;
    }

    return ret;
}
```


