# 004. Median of Two Sorted Arrays
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

[LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays)

### Example 1:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

### Example 2:
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

### Example 3:
```
Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000
```

# 004. 尋找兩個正序數組的中位數
給定兩個大小分別為 m 和 n 的正序（從小到大）數組 nums1 和 nums2。請你找出並返回這兩個正序數組的 中位數


## Solution  

### C++

```
#include <vector>
#include <stack>
#include <cmath>

using namespace std;

class Solution
{
public:
    double findKthElement(vector<int> &nums1, vector<int> &nums2, int target)
    {
        int len1 = nums1.size();
        int len2 = nums2.size();
        int startId1 = 0;
        int startId2 = 0;

        while (true)
        {
            /* cases break while loop*/
            if (startId1 == len1)
                return nums2[startId2 + target - 1];
            else if (startId2 == len2)
                return nums1[startId1 + target - 1];
            else if (target == 1)
                return min(nums1[startId1], nums2[startId2]);

            /* remove target/2 elements from the list*/
            int offset = target / 2 - 1; /* compare offset th element in each vector  */
            int tmpId1 = min(startId1 + offset, len1 - 1);
            int tmpId2 = min(startId2 + offset, len2 - 1);
            if (nums1[tmpId1] <= nums2[tmpId2])
            {
                target = target - (tmpId1 - startId1 + 1);
                startId1 = tmpId1 + 1;
            }
            else
            {
                target = target - (tmpId2 - startId2 + 1);
                startId2 = tmpId2 + 1;
            }
        }

        return 0.0;
    }

    double findMedianSortedArrays(vector<int> &nums1, vector<int> &nums2)
    {

        int totalLen = nums1.size() + nums2.size();
        double ret = 0.0;

        /* if totalLen is odd*/
        int KthElement = totalLen / 2 + 1;
        if (totalLen % 2 == 1)
            ret = findKthElement(nums1, nums2, totalLen / 2 + 1);
        else
            ret = (findKthElement(nums1, nums2, totalLen / 2) + findKthElement(nums1, nums2, totalLen / 2 + 1)) / 2;

        return ret;
    }
};

int main()
{
    vector<int> input1 = {2, 3, 4, 5, 6};
    vector<int> input2 = {1};

    Solution test;
    double res = test.findMedianSortedArrays(input1, input2);

    return 0;
}
```