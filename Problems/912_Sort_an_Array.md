# 912. Sort an Array

Given an array of integers nums, sort the array in ascending order.

给你一个整數數组 nums，請你將該數組升序排列。

[LeetCode](https://leetcode-cn.com/problems/sort-an-array)

### Example 1:
```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Example 2:
```

### Example 2:
```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```



* 1 <= nums.length <= 5 * 10^4
* -5 * 104 <= nums[i] <= 5 * 10^4

### Example 1

```
輸入：nums = [10,26,30,31,47,60], target = 40
輸出：[10,30] 或者 [30,10]
```

### Example 2

```
輸入：nums = [2,7,11,15], target = 9
輸出：[2,7] 或者 [7,2]

```

* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^6

## Solution  

### C++

* 時間複雜度：(nlogn )  由於歸並排序每次都將當前待排序的序列折半成兩個子序列遞歸調用，然後再合並兩個有序的子序列，
                       而每次合並兩個有序的子序列需要O(n) 的時間覆雜度，所以我們可以列出歸並排序運行時間 T(n) 的遞歸表達式：
                       T(n)=2T(2/n)+O(n) 根據主定理我們可以得出歸並排序的時間覆雜度為 O(nlogn)。

* 空間複雜度：O(n)      我們需要額外O(n) 空間的 tmp 數組，且歸並排序遞歸調用的層數最深為 log  n，所以我們還需要額外的O(log n) 的棧空間
                       所需的空間覆雜度即為 O(n+log n)=O(n)。

```
#include <vector>

using namespace std;

class Solution
{
private:
    vector<int> tmp;
    void mergeSort(vector<int> &nums, int left, int right)
    {
        if (right == left)
            return;

        int mid = left + (right - left) / 2;
        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);

        int startLeft = left;
        int startRight = mid + 1;
        int tmpStart = left;

        while (startLeft <= mid && startRight <= right)
        {
            if (nums[startLeft] <= nums[startRight])
                tmp[tmpStart++] = nums[startLeft++];
            else
                tmp[tmpStart++] = nums[startRight++];
        }

        while (startLeft <= mid)
            tmp[tmpStart++] = nums[startLeft++];

        while (startRight <= right)
            tmp[tmpStart++] = nums[startRight++];

        while (left <= right)
        {
            nums[left] = tmp[left];
            left++;
        }
    }

public:
    vector<int> sortArray(vector<int> &nums)
    {
        int len = nums.size();
        if (len == 1)
            return nums;

        tmp.resize(len);
        mergeSort(nums, 0, len - 1);

        return tmp;
    }
};

int main()
{
    /* input*/
    vector<int> input = {4, 2, 3};

    /* Test*/
    Solution test;
    vector<int> res = test.sortArray(input);

    return 0;
}
```