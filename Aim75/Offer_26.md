# 劍指 Offer 26 樹的子結構

輸入兩棵二叉樹A和B，判斷B是不是A的子結構。(約定空樹不是任意一個樹的子結構)

B是A的子結構， 即 A中有出現和B相同的結構和節點值。

 
[LeetCode](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)


### Example 1
Tree A
```
     3
    / \
   4   5
  / \
 1   2
```
Tree B：

```
   4 
  /
 1
```
返回 true，因为 B 與 A 的一個子樹有相同的結構和節點值。

* 0 <= 節點數 <= 10000

## Solution  


### C++

* 時間複雜度: O(m+n) 

* 空間複雜度: O(m) 


```
/* Definition for singly-linked list. */
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution
{
private:
    int target{0};
    bool match{false};
    TreeNode *startOri{nullptr};

    void countChainLen(TreeNode *head, int &len)
    {
        if (head == nullptr)
            return;

        len++;
        countChainLen(head->left, len);
        countChainLen(head->right, len);

        return;
    }

    void cmpChains(TreeNode *A, TreeNode *B, int &count)
    {
        /* stop condition*/
        if (A == nullptr && B != nullptr)
        {
            count = 0;
            return;
        }
        else if (A != nullptr && B == nullptr)
            return;
        else if (A == nullptr && B == nullptr)
            return;

        /* if current nodes' values are different*/
        if (A->val != B->val)
        {
            count = 0;
            cmpChains(A->left, startOri, count);
            if (match != true)
                cmpChains(A->right, startOri, count);
        }
        else /* current nodes' values  are the same*/
        {
            count++;
            if (count == target)
                match = true;
            if (match != true)
                cmpChains(A->left, B->left, count);
            if (match != true && count != 0)
                cmpChains(A->right, B->right, count);
        }
    }

public:
    bool isSubStructure(TreeNode *A, TreeNode *B)
    {
        startOri = B;

        /* len of chain B*/
        countChainLen(B, target);

        int count = 0;

        cmpChains(A, B, count);    

        return match;
    }
};

int main()
{
    /* input*/
    TreeNode A(3), B(4), C(5), D(1), E(2);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    B.right = &E;

    TreeNode F(4), G(1);
    F.left = &G;
    

    /* Test*/
    Solution test;
    bool res = test.isSubStructure(&A, &F);

    return 0;
}
```