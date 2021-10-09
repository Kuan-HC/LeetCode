# 面試金典 1621 交換和

給定兩個整數數組，請交換一對數值（每個數組中取一個數值），使得兩個數組所有元素的和相等。

返回一個數組，第一個元素是第一個數組中要交換的元素，第二個元素是第二個數組中要交換的元素。若有多個答案，返回任意一個均可。若無滿足條件的數值，返回空數組。

## Sum Swap

Given two arrays of integers, find a pair of values (one value from each array) that you can swap to give the two arrays the same sum.

Return an array, where the first element is the element in the first array that will be swapped, and the second element is another one in the second array. 
If there are more than one answers, return any one of them. If there is no answer, return an empty array.


[LeetCode](https://leetcode-cn.com/problems/sum-swap-lcci)

### Example 1
```
Input: array1 = [4, 1, 2, 1, 1, 2], array2 = [3, 6, 3, 3]
Output: [1, 3]
```

### C++ 


```
class Solution
{
public:
    vector<int> findSwapValues(vector<int> &array1, vector<int> &array2)
    {
        unordered_set<int> inventory;
        int sumTotal = 0;
        int sumArray1 = 0;

        for (const int &num : array1)
        {
            inventory.insert(num);
            sumTotal += num;
        }
        sumArray1 = sumTotal;
        for (const int &num : array2)
            sumTotal += num;

        if (sumTotal & 1 != 0)
            return {};

        const int diff = (sumTotal >> 1) - (sumTotal - sumArray1);
        for (const int &num : array2)
        {
            if (inventory.find(num + diff) != inventory.end())
                return {num + diff, num};
        }

        return {};
    }
};

int main()
{
    /* input */
    vector<int> input = {1, 2, 3};
    vector<int> input2 = {4, 5, 6};

    /* Test */
    Solution test;
    vector<int> res = test.findSwapValues(input, input2);

    return 0;
}
```
