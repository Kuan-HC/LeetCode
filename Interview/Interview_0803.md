# 面試金典 0803 魔術索引

在數組A[0...n-1]中，有所謂的魔術索引，滿足條件A[i] = i。給定一個有序整數數組，編寫一種方法找出魔術索引，若有的話，在數組A中找出一個魔術索引，
如果沒有，則返回-1。若有多個魔術索引，返回索引值最小的一個

 
##  Magic Index

A magic index in an array A[0...n-1] is defined to be an index such that A[i] = i. Given a sorted array of integers, write a method to find a magic index, if one exists, in array A. If not, return -1. If there are more than one magic index, return the smallest on


[LeetCode](https://leetcode-cn.com/problems/magic-index-lcci)


### Example 1

```
Input: nums = [0, 2, 3, 4, 5]
Output: 0
```

### Example 2

```
Input: nums = [1, 1, 1]
Output: 1
```

### C++ 

* 時間複雜度 O( log n) 

* 空間複雜度 O(n)

```
#include <vector>

using namespace std;
class Solution {
private:
    
    int recursion(vector<int>& nums, int leftLim, int rightLim)
    {   
        if(leftLim > rightLim)
            return -1;

        int mid = leftLim + (rightLim - leftLim) / 2;
        /* search left part first*/
        int left = recursion(nums, leftLim, mid - 1);
        if(left != -1)
            return left;
        else if (nums[mid] == mid)
            return mid;

        return recursion(nums, mid + 1, rightLim);        
    }
public:
    int findMagicIndex(vector<int>& nums) {
        /* 為何此題不能用二分查找？*/

        int left = 0;
        int right = nums.size() - 1;

        return recursion(nums, left, right);
    }
};

int main(void)
{
	/* input*/
	vector<int> input = {0,2,3,4,5};

	/* test*/
	Solution test;
	int res = test.findMagicIndex(input);

	return 0;
}
```
