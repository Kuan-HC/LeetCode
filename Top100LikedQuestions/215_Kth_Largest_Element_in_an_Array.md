# 215. Kth Largest Element in an Array

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

[LeetCode](https://leetcode.com/problems/kth-largest-element-in-an-array)

### Example 1:
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

### Example 2:
```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

# 數組中的第K個最大元素
在未排序的數組中找到第 k 個最大的元素。請注意，你需要找的是數組排序後的第 k 個最大的元素，而不是第 k 個不同的元素。


## Solution  
* Heap sort
[WIKI](https://en.wikipedia.org/wiki/Heapsort)

### C

```
void swap(int *a, int *b)
{
  int tmp = *a;
  *a = *b;
  *b = tmp;
}

void heapify(int *nums, int idx, int numsSize)
{
  int largest = idx;
  int left = idx * 2 + 1;
  int right = idx * 2 + 2;

  if (left < numsSize && nums[left] > nums[largest])
    largest = left;

  if (right < numsSize && nums[right] > nums[largest])
    largest = right;

  if (largest != idx)
  {
    swap(&nums[largest], &nums[idx]);
    heapify(nums, largest, numsSize);
  }
}

int findKthLargest(int *nums, int numsSize, int k)
{
  /**
   * TODO: transfor array into heap
   * */
  int i = 0;
  for (i = numsSize / 2 - 1; i >= 0; --i)
    heapify(nums, i, numsSize);
  /* array has heapified, so the larget value is no at num[0] */

  /**
   * TODO: find the Kth largest element
   */
  for (i = 0; i < k - 1; ++i)
  {
    swap(&nums[0], &nums[numsSize - 1 - i]);
    heapify(nums, 0, numsSize-i-1);
  }

  return nums[0];
}

int main()
{

  int nums[] = {3, 2, 1, 5, 6, 4};

  int ans = findKthLargest(nums, sizeof(nums) / sizeof(nums[0]), 2);

  return 0;
}
```
