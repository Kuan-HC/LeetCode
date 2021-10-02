# 面試金典 1705 字母與數字

給定一個放有字母和數字的數組，找到最長的子數組，且包含的字母和數字的個數相同。

返回該子數組，若存在多個最長子數組，返回左端點下標值最小的子數組。若不存在這樣的數組，返回一個空數組。

## Find Longest Subarray

Given an array filled with letters and numbers, find the longest subarray with an equal number of letters and numbers.

Return the subarray. If there are more than one answer, return the one which has the smallest index of its left endpoint. If there is no answer, return an empty arrary.

[LeetCode](https://leetcode-cn.com/problems/find-longest-subarray-lcci/)

### Example 1
```
Input: ["A","1","B","C","D","2","3","4","E","5","F","G","6","7","H","I","J","K","L","M"]

Output: ["A","1","B","C","D","2","3","4","E","5","F","G","6","7"]

```

### C++ 


```
#include <vector>
#include <unordered_map>
#include <string>

using namespace std;

class Solution
{
public:
    vector<string> findLongestSubarray(vector<string> &array)
    {
        int len = array.size();
        if (len <= 1)
            return {};

        /* prefix*/

        int maxLen = 0; // first is balance, second is position
        pair<int, int> maxLandR = make_pair(0, 0);

        unordered_map<int, int> prefix;
        int balance = 0; // position mean letter more and vice versa
        prefix[0] = 0;

        for (int i = 0; i < len; i++)
        {
            if (array[i][0] >= 48 && array[i][0] <= 57) // digit
                balance--;
            else
                balance++;

            if (prefix.find(balance) != prefix.end())
            {
                int len = i - prefix[balance] + 1;
                if (len > maxLen)
                {
                    maxLen = len;
                    maxLandR.first = prefix[balance];
                    maxLandR.second = i + 1;  // why i + 1, for xxx.begin() + second
                }
            }
            else
            {
                prefix[balance] = i + 1;
            }
        }

        vector<string> ret(array.begin() + maxLandR.first, array.begin() + maxLandR.second);
        return ret;
    }
};

int main()
{
    vector<string> input = {"A","1","B","C","D","2","3","4","E","5","F","G","6","7","H","I","J","K","L","M"};
    Solution test;
    
    test.findLongestSubarray(input);

    return 0;
}
```
