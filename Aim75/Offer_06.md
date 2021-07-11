# 劍指 Offer 06 從頭到尾打印鍊表

輸入一個鍊表的頭節點，從尾到頭反過來返回每個節點的值(用數組返回)。
 
[LeetCode](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)


### Example 1
```
輸入：head = [1,3,2]
輸出：[2,3,1]
```

* 0 <= 鍊表長度 <= 10000

## Solution  


### C++

* 時間覆雜度: O(n) 

* 空間覆雜度: O(n) 

```
#include <vector>

using namespace std;

/**
 * Definition for singly-linked list.*/
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
private:
    void recursion(ListNode *head, vector<int> &record)
    {
        if (head == nullptr)            
            return;        

        recursion(head->next, record);
        record.push_back(head->val);
    }

public:
    vector<int> reversePrint(ListNode *head)
    {          
        vector<int> result;
        recursion(head, result);

        return result;
    }
};

int main()
{
    /* input*/
    ListNode A(1), B(2), C(3);
    A.next = &B;
    B.next = &C;

    Solution test;
    vector<int> res = test.reversePrint(nullptr);

    return 0;
}
```

### C

```
#include <stdlib.h>

/**
 * Definition for singly-linked list.*/
struct ListNode
{
    int val;
    struct ListNode *next;   
};

void recursion(struct ListNode *head, int **start, int *returnSize, int *count)
{
    if (head == NULL)
    {
        int *resultArray = (int *)malloc(sizeof(int) * (*returnSize));
        *start = resultArray;
        return;
    }
    (*returnSize)++;
    recursion(head->next, start, returnSize, count);
    (*start)[(*count)++] = head->val;
}

int *reversePrint(struct ListNode *head, int *returnSize)
{
    *returnSize = 0;
    int **start = (int **)malloc(sizeof(int *));
    int count = 0;


    recursion(head, start, returnSize, &count);

    return *start;
}

int main()
{
    /* input*/
    struct ListNode A, B;
    A.val = 1;
    A.next = &B;
    B.val = 2;
    B.next = NULL;
    
    

    int returnSize = 0;
    int *res = reversePrint(&A, &returnSize);

    for (int i = 0; i < returnSize; ++i)
        printf(" %i,", res[i]);

    return 0;
}
```