# 劍指 Offer 18 刪除鏈表的節點

給定單向鏈表的頭指針和一個要刪除的節點的值，定義一個函數刪除該節點。

返回刪除後的鏈表的頭節點。

[LeetCode](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

### Example 1

```
輸入: head = [4,5,1,9], val = 5
輸出: [4,1,9]
解釋: 給定你鏈表中值為 5 的第二個節點，那麼在調用了你的函數之後，該鏈表應變為 4 -> 1 -> 9.
```

### Example 2

```
輸入: head = [4,5,1,9], val = 1
輸出: [4,5,9]
解釋: 給定你鏈表中值為 1 的第三個節點，那麽在調用了你的函數之後，該鏈表應變為 4 -> 5 -> 9.
```

* 題目保證鏈表中節點的值互不相同
* 若使用 C 或 C++ 語言，你不需要 free 或 delete 被刪除的節點
 
## Solution  


### C++

* 時間複雜度：O(n) 其中n是鍊表的長度，需要遍曆鍊表一次。

* 空間複雜度：O(1) 


```
/* Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
public:
    ListNode *deleteNode(ListNode *head, int val)
    {
        ListNode retHead(0);
        ListNode *tmpHead = &retHead;

        while (head != nullptr)
        {
            if ( head->val == val)
                head = head->next;                                  
            
            tmpHead->next = head;         
            tmpHead = tmpHead->next;
            if(head != nullptr)
                head = head->next;  
        }

        return retHead.next;
    }
};
int main()
{
    /* input*/
    ListNode A(1), B(3), C(5);
    A.next = &B;
    B.next = &C;

    /* Test*/
    Solution test;
    ListNode *res = test.deleteNode(&A, 3);

    return 0;
}
```