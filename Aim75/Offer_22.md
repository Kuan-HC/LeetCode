# 劍指 Offer 22 鏈表中倒數第k個節點

輸入一個鏈表，輸出該鏈表中倒數第k個節點。為了符合大多數人的習慣，本題從1開始計數，即鏈表的尾節點是倒數第1個節點。

例如，一個鏈表有 6 個節點，從頭節點開始，它們的值依次是 1、2、3、4、5、6。這個鏈表的倒數第 3 個節點是值為 4 的節點。

[LeetCode](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)


### Example 1

```
给定一个鍊表: 1->2->3->4->5, 和 k = 2.

返回鍊表 4->5.

```

## Solution  


### C++

* 時間覆雜度: O(n) 

* 空間覆雜度: O(1) 


```
/*
  Definition for singly-linked list.*/
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
private:
    void recursion(ListNode *root)
    {
        if (root == nullptr)
            return;

        recursion(root->next);
    }

public:
    ListNode *getKthFromEnd(ListNode *head, int k)
    {
        ListNode *second = head;

        while (k-- != 0)
            head = head->next;
        

        while (head != nullptr)
        {
            head = head->next;
            second = second->next;
        }

        return second;
    }
};

int main()
{
    /* input*/
    ListNode A(1), B(2), C(3), D(4);
    A.next = &B;
    B.next = &C;
    C.next = &D;

    /* Test*/
    Solution test;
    ListNode *res = test.getKthFromEnd(&A, 2);

    return 0;
}
```