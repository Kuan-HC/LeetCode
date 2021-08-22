# 002. Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

[LeetCode](https://leetcode.com/problems/add-two-numbers/)

<img src="img/002.jpg" width = "400"/>

### Example 1:
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```
### Example 2:
```
Input: l1 = [0], l2 = [0]
Output: [0]
```
### Example 3:
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

### Constraints
* The number of nodes in each linked list is in the range [1, 100].
* 0 <= Node.val <= 9
* It is guaranteed that the list represents a number that does not have leading zeros.


#  兩數相加
給你兩個 非空 的鏈表，表示兩個非負的整數。它們每位數字都是按照 逆序 的方式存儲的，並且每個節點只能存儲 一位 數字。

請你將兩個數相加，並以相同形式返回一個表示和的鏈表。

你可以假設除了數字 0 之外，這兩個數都不會以 0 開頭

## Solution  

### C++

* 時間複雜度 O(n) 鍊表的長度

* 空間複雜度 O(n) 需要建立額外長度n的節點


```
struct ListNode
{
    ListNode *next;
    int value;

    ListNode(int a) : next(nullptr), value(a){};
};

class Solution
{
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2)
    {
        ListNode head(0);
        ListNode *tail = &head;

        int digit = 0;
        int overTen = 0;
        while (l1 != nullptr || l2 != nullptr)
        {
            digit = overTen;

            if (l1 != nullptr)
            {
                digit += l1->value;
                l1 = l1->next;
            }
            if (l2 != nullptr)
            {
                digit += l2->value;
                l2 = l2 -> next;
            }

            ListNode *tmp = new ListNode(digit % 10);
            tail->next = tmp;
            tail = tail->next;

            overTen = digit / 10;
        }

        return head.next;
    }
};

int main()
{
    /*input*/
    ListNode A(2), B(4), C(3);
    A.next = &B;
    B.next = &C;

    ListNode D(5), E(6), F(4);
    D.next = &E;
    E.next = &F;

    /* unit test*/
    Solution test;
    ListNode *res = test.addTwoNumbers(&A, &D);

    return 0;
}
```

### C

```
struct ListNode *addTwoNumbers(struct ListNode *l1, struct ListNode *l2)
{
    struct ListNode *head = NULL;
    struct ListNode *tmp = NULL;
    struct ListNode *start = NULL;

    int initialized = 0;
    int dig_1 = 0;
    int dig_2 = 0;
    int nextPlusOne = 0;

    while (l1 != NULL || l2 != NULL || nextPlusOne == 1)
    {
        dig_1 = l1 ? l1->val : 0;
        dig_2 = l2 ? l2->val : 0;

        tmp = (struct ListNode *)malloc(sizeof(struct ListNode));
        tmp->next = NULL;

        tmp->val = dig_1 + dig_2 + nextPlusOne;
        nextPlusOne = 0;

        if (tmp->val > 9)
        {
            tmp->val %= 10;
            nextPlusOne = 1;
        }

        l1 = l1 ? l1->next : NULL;
        l2 = l2 ? l2->next : NULL;

        if (initialized == 0)
        {
            start = tmp;
            head = tmp;
            initialized = 1;
        }
        else
        {
            head->next = tmp;
            head = head->next;
        }
    }

    return start;
}
```


