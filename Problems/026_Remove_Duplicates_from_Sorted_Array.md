# Remove Duplicates from Sorted Array
Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.  
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

### Example 1:
```
Input: nums = [1,1,2]
Output: 2, nums = [1,2]
Explanation: Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the returned length.
```

 
### C

* 時間複雜度 O(N)
* 空間複雜度 O(1)
```
int removeDuplicates(int* nums, int numsSize){
    if(numsSize == 0 )
        return 0;

    int j = 0;    
    for (int i = 1; i < numsSize; i++)
    {
        if (nums[i] != nums[j])
        {
            j++;
            nums[j] = nums[i];
        }
    }

    return j+1;
}
```

### C++
```
class Solution {
public:
    int removeDuplicates(vector<int>& nums)
    {
        int&& len = nums.size();
        if(len <= 1)
            return len;
        
        int ptrL = 0;
        for(int i = 1; i < len; ++i)
        {
            if(nums[i] != nums[ptrL])
            {
                ++ptrL;
                nums[ptrL] = nums[i];
            }
        }

        return ptrL + 1;
    }
};
```
