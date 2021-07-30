# 297. Serialize and Deserialize Binary Tree
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

[LeetCode](https://leetcode.com/problems/serialize-and-deserialize-binary-tree)

### Example 1:

<img src="img/297_q.jpg" width = "500"/>

```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```

### Example 2:
```
Input: root = []
Output: []
```

### Example 3:
```
Input: root = [1]
Output: [1]
```
### Constraints

* The number of nodes in the tree is in the range [0, 10^4].
* -1000 <= Node.val <= 1000

#  二叉樹的序列化與反序列化

序列化是將一個數據結構或者對象轉換為連續的比特位的操作，進而可以將轉換後的數據存儲在一個文件或者內存中，同時也可以通過網絡傳輸到另一個計算機環境，采取相反方式重構得到原數據。

請設計一個算法來實現二叉樹的序列化與反序列化。這里不限定你的序列 / 反序列化算法執行邏輯，你只需要保證一個二叉樹可以被序列化為一個字符串並且將這個字符串反序列化為原始的樹結構。




## Solution  


### C++
<img src="img/297.gif" width = "600"/>

```
#include <vector>
#include <string>

using namespace std;

/**
 * Definition for a binary tree node.*/
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

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
    /* Input*/
    TreeNode B(2), D(4), E(5);
    TreeNode C(3, &D, &E);

    TreeNode A(100, &B, &C);

    /* unit test*/
    Codec ser, deser;
    string retS = ser.serialize(&A);

    TreeNode *ans = deser.deserialize(ser.serialize(&A));

    return 0;
}
```


