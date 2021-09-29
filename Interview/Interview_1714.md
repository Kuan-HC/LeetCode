# 面試金典 1714 最小k個數

設計一個算法，找出數組中最小的k個數。以任意順序返回這k個數均可。

## Smallest K

Design an algorithm to find the smallest K numbers in an array.
 
[LeetCode](https://leetcode-cn.com/problems/smallest-k-lcci/)

### Example 1
```
Input:  arr = [1,3,5,7,2,4,6,8], k = 4
Output:  [1,2,3,4]

```

* 0 <= len(arr) <= 100000
* 0 <= k <= min(100000, len(arr))

### C++ 


```
class Solution {
public:
    vector<int> smallestK(vector<int>& arr, int k) {
        if( k == 0 || arr.size() == 0)
            return {};
        priority_queue<int> bigHeap;
        vector<int> ret;

        for(const int& num: arr)
        {
            if(bigHeap.size() < k)
            {
                bigHeap.push(num);
            }
            else if(num < bigHeap.top())
            {
                bigHeap.pop();
                bigHeap.push(num);
            }            
        }

        for(int i = 0; i < k; ++i)
        {   
            ret.push_back(bigHeap.top());
            bigHeap.pop();
        }


        return ret;
    }
};

int main(void)
{
    /* input*/
    vector<int> input  = {1,3,5,7,2,4,6,8};
    

    Solution test;
    vector<int> res = test.smallestK(input, 4);

    return 0;
}
```
