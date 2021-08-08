# 面試金典 0206 編寫一個函數，檢查輸入的鏈表是否是回文的。

[LeetCode](https://leetcode-cn.com/problems/palindrome-linked-list-lcci/)

### Example 1
```
輸入： 1->2
輸出： false 
```

### Example 1
```
輸入： 1->2->2->1
輸出： true 
```

進階：
你能否用 O(n) 時間覆雜度和 O(1) 空間覆雜度解決此題？

### C++

* 時間複雜度：o(n) 需先遍曆鍊表，將前一半逆序，需時n，之後將一半的鍊錶比對，需時 n/2

* 空間複雜度：o(1) 

```
class Solution
{
public:
    bool isPalindrome(ListNode *head)
    {
        if (head == nullptr)
            return true;

        bool odd = false;

        ListNode *center = head;
        ListNode *revHead = nullptr;

        while (head != nullptr)
        {
            /* find the center node, while odd is not ture, 
               center not represent the right node next to real center
                Also, the nodes left to center are reversed 
            */

            odd = odd == true ? false : true;
            if (odd != true)
            {
                ListNode *tmp = center;
                center = center->next;
                tmp->next = revHead;
                revHead = tmp;
            }
            head = head->next;
        }

        if (odd == true)
            center = center->next;    

        while (revHead != nullptr && center != nullptr)
        {
            if (revHead->val != center->val)
                return false;

            revHead = revHead->next;
            center = center->next;
        }

        return true;
    }
};
```
