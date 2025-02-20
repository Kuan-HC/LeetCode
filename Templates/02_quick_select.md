# Quick Select 快速選擇

快速選擇算法（QuickSelect），也被稱為“快速選擇”，是一種用於選擇數組中第 k 大元素或第 k 小元素的算法。它的時間複雜度平均為 O(n)，最壞情況下為 O(n^2)。

以下是其基本步驟：

1. 選擇一個樞紐（pivot），通常是數組中的最後一個元素。

2. 將數組分為兩部分：一部分元素小於樞紐，另一部分元素大於樞紐。

3. 根據 k 的值，決定繼續在那部分中搜尋：

    如果 k 小於或等於左部分的長度，則在左部分中繼續搜索。  

    否則，在右部分中繼續搜索，並調整 k 的值。


### C++ 

```
int quickSelect(vector<int> &nums, const int &left, const int &right, const int &target)
{
    // 三素取中法
    int &&mid = left + ((right - left) >> 1);
    if (nums[left] > nums[mid])
        swap(nums[left], nums[mid]);
    if (nums[left] > nums[right])
        swap(nums[left], nums[right]);
    if (nums[mid] > nums[right])
        swap(nums[mid], nums[right]);
    swap(nums[mid], nums[right]);

    // 將數組分成大於小於pivot值
    int i = left;
    for (int j = left; j < right; ++j){
        if (nums[j] < nums[right])
            swap(nums[i++], nums[j]);
    }
    swap(nums[i], nums[right]);
    
    if (i == target)
        return nums[i];
    else if (i < target)
        return quickSelect(nums, i + 1, right, target);
    else
        return quickSelect(nums, left, i - 1, target);
}

int main(int argc, char **argv){

    vector<int> nums = {1, 2, 3, 4, 5, 6, 7};
    // 找出第二大的
    int k = 2;
    auto res = quickSelect(nums, 0, nums.size() - 1, nums.size() - k);

    return 0;
}
```