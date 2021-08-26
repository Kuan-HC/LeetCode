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

### C+++

* 空間複雜度 O(n)

* 時間複雜度 0(1)
```
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
public:
    bool isPalindrome(ListNode *head)
    {
        /* find the middle*/
        bool pause = true;
        ListNode *savedHead = head;
        ListNode *slow = head;

        while (head != nullptr)
        {
            head = head->next;
            if (pause != true)
                slow = slow->next;

            pause = pause == true ? false : true;
        }

        /* rever the list from slow*/
        ListNode *revHead = slow;
        ListNode *tmp = nullptr;

        while (slow != nullptr)
        {
            revHead = slow;
            slow = slow->next;
            revHead->next = tmp;
            tmp = revHead;
        }

        while (revHead != nullptr)
        {
            if (revHead->val == savedHead->val)
            {
                revHead = revHead->next;
                savedHead = savedHead->next;
            }
            else
                return false;
        }

        return true;
    }
};

int main()
{
    /* Input*/
    ListNode A(1), B(2), C(3), D(3), E(1);
    A.next = &B;
    B.next = &C;
    C.next = &D;
    D.next = &E;

    /* unit test*/
    Solution test;
    bool res = test.isPalindrome(&A);

    return 0;
}
```


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


