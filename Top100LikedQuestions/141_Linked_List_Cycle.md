# Linked List Cycle
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.



[LeetCode](https://leetcode.com/problems/linked-list-cycle/)  

### Example 1:
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```
### Example 2:
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```
# 環形鍊表
給定一個鏈表，判斷鏈表中是否有環。

如果鏈表中有某個節點，可以通過連續跟蹤 next 指針再次到達，則鏈表中存在環。 為了表示給定鏈表中的環，  
我們使用整數 pos 來表示鏈表尾連接到鏈表中的位置（索引從 0 開始）。 如果 pos 是 -1，則在該鏈表中沒有環。  

注意：pos 不作為參數進行傳遞，僅僅是為了標識鏈表的實際情況。

如果鏈表中存在環，則返回 true 。 否則，返回 false 。

# Solution

## C
```
bool hasCycle(struct ListNode *head) {
    struct ListNode *fast = head;
    struct ListNode *slow = head;
    
    while(fast != NULL){
        if (fast->next == NULL)
            return false;
        else   
            fast = fast->next;
            if (fast->next == NULL)
                return false;
            else{
                fast = fast->next;
                slow = slow ->next;
                if (fast == slow)
                    return true;
                }
    }
      
    return false;  
}
```


