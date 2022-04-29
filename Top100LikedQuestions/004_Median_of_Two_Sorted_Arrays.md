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

* 時間複雜度 O(log(min(m,n)))

```
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int&& nums1Len = nums1.size();
        int&& nums2Len = nums2.size();
        /* 中位數將一個數組切成兩半，若該數組是奇數，將中位數歸給左邊，同時左邊數組的最大值即為 中位數*/
        int&& odd = (nums1Len + nums2Len) & 1;
        const int targetLeftLen = (nums1Len + nums2Len) / 2 + odd;

        vector<int>& shortVec = nums1Len <= nums2Len? nums1 : nums2;
        vector<int>& longVec = nums2Len >= nums1Len? nums2 : nums1;

        /* Binary Search，猜有多少個在short中屬於左邊*/
        int left = 0;
        int right = shortVec.size();
        int mid = 0;
        int leftTop = 0;
        int rightTop = 0;
        while(left <= right){
            mid = left + (right - left) / 2;
            int&& shortLeftMax = mid == 0? INT_MIN : shortVec[mid - 1];
            int&& shortRightMin = mid == shortVec.size()? INT_MAX : shortVec[mid];
            int&& restLeft = targetLeftLen - mid;
            int&& longLeftMax = restLeft == 0 ? INT_MIN : longVec[restLeft -1];
            int&& longRightMin = restLeft == longVec.size()? INT_MAX : longVec[restLeft];

            if(shortLeftMax > longRightMin)
                right = mid - 1;
            else if(shortRightMin < longLeftMax)
                left = mid + 1;  
            else{
                leftTop = max(shortLeftMax, longLeftMax);
                rightTop = min(shortRightMin, longRightMin);
                if(odd == 1)
                    return leftTop;
                else
                    return (leftTop + rightTop) * 0.5;
            }      

        }       

        return 0;
    }
};
```