# 面試金典 1003 搜索旋轉數組

給定一個排序後的數組，包含n個整數，但這個數組已被旋轉過很多次了，次數不詳。請編寫代碼找出數組中的某個元素，假設數組元素原先是按升序排列的。若有多個相同元素，返回索引值最小的一個。
 
##  Search Rotate Array 

Given a sorted array of n integers that has been rotated an unknown number of times, write code to find an element in the array. You may assume that the array was originally sorted in increasing order. If there are more than one target elements in the array, return the smallest index.


[LeetCode](https://leetcode-cn.com/problems/search-rotate-array-lcci/)


### Example 1

```
Input: arr = [15, 16, 19, 20, 25, 1, 3, 4, 5, 7, 10, 14], target = 5
Output: 8 (the index of 5 in the array)
```

### Example 2

```
Input: arr = [15, 16, 19, 20, 25, 1, 3, 4, 5, 7, 10, 14], target = 11
 Output: -1 (not found)

```

### C++ 

```
class Solution
{
public:
	int search(vector<int> &nums, int target)
	{
		int len = nums.size();
		int left = 0;
		int right = len - 1;
		int mid = 0;

		while (left <= right) // 才能檢查 left == right時的值
		{
			mid = left + (right - left) / 2;

			if (nums[left] == target)
				return left;
			else if(nums[left] == nums[mid]) // 出現重覆原素, 處理左方，左方可以確定不會出現 1 1 2 1 1 1 1這種情形
				left++;                      
			else if (nums[mid] > nums[left]) // 左方是升序的
			{
				if (target >= nums[left] && nums[mid] >= target) //目標在左方區間
					right = mid;
				else
					left = mid + 1;
			}
			else // 右方是升序的
			{
				if (target >= nums[mid] && nums[right] >= target)
					left = mid;
				else
					right = mid - 1;
			}
		}

		return -1;
	}
};

int main(void)
{
	/* input*/
	vector<int> input = {15, 16, 19, 20, 25, 1, 3, 4, 5, 7, 10, 14};

	/* test*/
	Solution test;
	int res = test.search(input, 16);

	return 0;
}
```
