# 面試金典 1718 最短超串

假設你有兩個數組，一個長一個短，短的元素均不相同。找到長數組中包含短數組所有的元素的最短子數組，其出現順序無關緊要。

返回最短子數組的左端點和右端點，如有多個滿足條件的子數組，返回左端點最小的一個。若不存在，返回空數組。

## Shortest Supersequence

ou are given two arrays, one shorter (with all distinct elements) and one longer. 
Find the shortest subarray in the longer array that contains all the elements in the shorter array. The items can appear in any order.

Return the indexes of the leftmost and the rightmost elements of the array. 
If there are more than one answer, return the one that has the smallest left index. If there is no answer, return an empty array.

[LeetCode](https://leetcode-cn.com/problems/shortest-supersequence-lcci)

### Example 1
```
Input:
big = [7,5,9,0,2,1,3,5,7,9,1,1,5,8,8,9,7]
small = [1,5,9]
Output: [7,10]
```

### C++ 


```
class Solution
{
public:
    vector<int> shortestSeq(vector<int> &big, vector<int> &small)
    {
        unordered_map<int, int> base;
        int gap = small.size();
        for (const int &item : small)
            base[item] = 1;

        int left = 0;
        int right = 0;
        int minLen = INT_MAX;
        vector<int> ret;
        
        for (;right < big.size(); right++)
        {
            if (base.find(big[right]) != base.end())
            {
                if (base[big[right]] == 1)
                    gap--;
                 base[big[right]]--;
            }

            while (gap == 0){
                int tempLen = right - left + 1;
                if (tempLen < minLen){
                    ret = {left, right};
                    minLen = tempLen;
                }
                if (base.find(big[left]) != base.end() && base[big[left]]++ == 0)                   
                        gap++;                   
                left++;
            }
        }
        return ret;
    }
};

```
