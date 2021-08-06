# 面試金典 0201 移除重覆節點

編寫代碼，移除未排序鏈表中的重覆節點。保留最開始出現的節點。

[LeetCode](https://leetcode-cn.com/problems/remove-duplicate-node-lcci/)

### Example 1
```
 輸入：[1, 2, 3, 3, 2, 1]
 輸出：[1, 2, 3]
```

### Example 1
```
 輸入：[1, 1, 1, 1, 2]
 輸出：[1, 2]
```

* 鏈表長度在[0, 20000]範圍內。
* 鏈表元素在[0, 20000]範圍內。


### C++

* 時間複雜度：o(n log n) set 的插入需時 log n，最差的情形整個鍊表都無重覆

* 空間複雜度：o(n) 

```
#include <unordered_set>

using namespace std;

/*  Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
public:
    ListNode *removeDuplicateNodes(ListNode *head)
    {
        if (head == nullptr)
            return nullptr;

        unordered_set<int> intSet;

        ListNode start(0);
        ListNode *tail = &start;

        while (head != nullptr)
        {
            if (intSet.find(head->val) == intSet.end())
            { /* this node not exist yet*/
                tail->next = head;
                tail = tail->next;
                intSet.insert(head->val);
            }
            head = head->next;
        }
        tail->next = nullptr;

        return start.next;
    }
};

int main()
{
    /* input*/
    struct ListNode A(1), B(1), C(1), D(2), E(2);
    A.next = &B;
    B.next = &C;
    C.next = &D;
    D.next = &E;

    /* Test*/
    Solution test;
    ListNode *res = test.removeDuplicateNodes(&A);

    return 0;
}
```
