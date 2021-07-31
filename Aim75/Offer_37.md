# 劍指 Offer 65 二叉樹的序列化與反序列化

序列化是將一個數據結構或者對象轉換為連續的比特位的操作，進而可以將轉換後的數據存儲在一個文件或者內存中，同時也可以通過網絡傳輸到另一個計算機環境，采取相反方式重構得到原數據。

請設計一個算法來實現二叉樹的序列化與反序列化。這里不限定你的序列 / 反序列化算法執行邏輯，你只需要保證一個二叉樹可以被序列化為一個字符串並且將這個字符串反序列化為原始的樹結構。

[LeetCode](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

### Example 1:

```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```


## Solution  



### C++

* 時間複雜度：在序列化和反序列化函數中，我們只訪問每個節點一次，因此時間覆雜度為 O(n)，其中 n 是節點數，即樹的大小。

* 空間複雜度：在序列化和反序列化函數中，我們遞歸會使用棧空間，故漸進空間覆雜度為 O(n)。



```
#include <string>
#include <queue>

using namespace std;

/* Definition for a binary tree node. */
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

/* Definition for a binary tree node. */
class Codec
{
private:
    void dfsSerialize(TreeNode *root, string &ret)
    {
        if (root == nullptr)
        {
            ret += "-,";
            return;
        }

        ret += to_string(root->val) + ',';

        dfsSerialize(root->left, ret);
        dfsSerialize(root->right, ret);
    }

    TreeNode *dfsDeserialize(queue<string> &data)
    {
        string test = data.front();
        data.pop();

        TreeNode *root = nullptr;
        if (test != "-")
        {
            root = new TreeNode(stoi(test));
            /* left branch*/
            root->left = dfsDeserialize(data);
            /* right branch*/
            root->right = dfsDeserialize(data);
        }

        return root;
    }

public:
    // Encodes a tree to a single string.
    string serialize(TreeNode *root)
    {
        string ret;
        dfsSerialize(root, ret);
        return ret;
    }

    // Decodes your encoded data to tree.
    TreeNode *deserialize(string data)
    {
        queue<string> stringInput;
        string tmp;
        for (const auto &c : data)
        {
            if (c == ',')
            {
                stringInput.emplace(tmp);
                tmp.clear();
                continue;
            }
            tmp += c;
        }

        TreeNode *root = dfsDeserialize(stringInput);
        return root;
    }
};

int main()
{
    /* input*/
    TreeNode A(1), B(2), C(3), D(4);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    /* Test*/
    Codec test;
    TreeNode *res = test.deserialize(test.serialize(&A));
    

    return 0;
}
```