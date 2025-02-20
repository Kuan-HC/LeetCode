# Quick Select 快速選擇 II

對於包含大量重覆元素的數組，每輪的哨兵劃分都可能將數組劃分為長度為1和n−1的兩個部分，這種情況下快速排序的時間覆雜度會退化至O(N<sup>2<sup>)  

一種解決方案是使用「三路劃分」，即每輪將數組劃分為三個部分：小於、等於和大於基準數的所有元素。這樣當發現第k大數字處在“等於基準數”的子數組中時，便可以直接返回該元素。  

為了進一步提升算法的穩健性，我們采用隨機選擇的方式來選定基準數。



### C++ 

```
class Solution {
protected:
    random_device rd;
    mt19937 mt{rd()};
    int quickSelect(vector<int>& nums, const int& k){
        const int& pivot = nums[mt() % nums.size()];
        vector<int> small, equal, big;
        for(int& num : nums){
            if(num > pivot)
                big.push_back(num);
            else if(num < pivot)
                small.push_back(num);
            else 
                equal.push_back(num);
        }

        if(k <= big.size())
            return quickSelect(big, k);
        else if(k > nums.size() - small.size())
            return quickSelect(small, k - nums.size() + small.size());
        return pivot;
    }
    
public:
    int findKthLargest(vector<int>& nums, int k) {
        return quickSelect(nums, k);
    }
};


int main(int argc, char **argv){
    vector<int> nums = {1, 2, 3, 4, 5, 6, 7};

    Solution test;
    // 找出第二大的
    int k = 2;
    auto res = test.quickSelect(nums, 2);

    return 0;
}
```