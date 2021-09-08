# 面試金典 0205 鏈表求和

給定兩個用鏈表表示的整數，每個節點包含一個數位。

這些數位是反向存放的，也就是個位排在鏈表首部。

編寫函數對這兩個整數求和，並用鏈表形式返回結果。

##  Sum Lists

You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

[LeetCode](https://leetcode-cn.com/problems/sum-lists-lcci/)

### Example 1

```
入：(7 -> 1 -> 6) + (5 -> 9 -> 2)，即617 + 295
輸出：2 -> 1 -> 9，即912

```

### C++ 

* 時間複雜度 O(n) n為鍊表的最大長度

* 空間複雜度 O(1)

```
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
private:
    ListNode *singleNode(ListNode *root, int val)
    {
        if (root == nullptr && val == 0)
            return nullptr;
        else if (root == nullptr && val != 0)
            return new ListNode(val);

        int rootVal = root->val + val;
        root->val = rootVal % 10;

        root->next = singleNode(root->next, rootVal / 10);

        return root;
    }
    ListNode *nodeAdd(ListNode *l1, ListNode *l2, int val)
    {
        if (l1 == nullptr || l2 == nullptr)
        {
            ListNode *tmp = l1 == nullptr ? l2 : l1;
            return singleNode(tmp, val);
        }

        int tempVal = l1->val + l2->val + val;
        l1->val = tempVal % 10;
        l1->next = nodeAdd(l1->next, l2->next, tempVal / 10);

        return l1;
    }

public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2)
    {
        if (l1 == nullptr || l2 == nullptr)
            return l1 == nullptr ? l2 : l1;

        return nodeAdd(l1, l2, 0);
    }
};

int main()
{
    ListNode A(9), B(9), C(9);
    ListNode D(3), E(9), F(2);
    A.next = &B;
    B.next = &C;

    D.next = &E;
    E.next = &F;

    Solution test;
    ListNode *res = test.addTwoNumbers(&A, &D);

    return 0;
}
```
