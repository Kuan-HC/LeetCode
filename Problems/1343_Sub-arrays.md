# 1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold

給你一個整數數組 arr 和兩個整數 k 和 threshold 。

請你返回長度為 k 且平均值大於等於 threshold 的子數組數目。

[LeetCode](https://leetcode-cn.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold)

### Example 1:
```
輸入：arr = [2,2,2,2,5,5,5,8], k = 3, threshold = 4
輸出：3
解釋：子數組 [2,5,5],[5,5,5] 和 [5,5,8] 的平均值分別為 4，5 和 6 。其他長度為 3 的子數組的平均值都小於 4 （threshold 的值)。
```

### Example 2:
```
輸入：arr = [1,1,1,1,1], k = 1, threshold = 0
輸出：5
```

### Example 3:
```
輸入：arr = [11,13,17,23,29,31,7,5,2,3], k = 3, threshold = 5
輸出：6
解釋：前 6 個長度為 3 的子數組平均值都大於 5 。注意平均值不是整數。
```

### Example 4:
```
輸入：arr = [7,7,7,7,7,7,7], k = 7, threshold = 7
輸出：1
```

* 1 <= arr.length <= 10^5
* 1 <= arr[i] <= 10^4
* 1 <= k <= arr.length
* 0 <= threshold <= 10^4



## Solution  

### C++

* 時間複雜度：O(n)   需執行鍊表長度 + 1次  空間複雜度 n

* 空間複雜度：O(n)   需鍊表長度+1的空間

```
#include <vector>

using namespace std;

class Solution
{
public:
  int numOfSubarrays(vector<int> &arr, int k, int threshold)
  {
    int len = arr.size();
    if (k > len)
      return 0;

    int target = k * threshold;
    int count = 0;
    vector<int> prefix(len + 1, 0);

    for (int i = 1; i <= len; ++i)
    {
      prefix[i] = arr[i - 1] + prefix[i - 1];
      if(( i >= k) && (prefix[i] - prefix[i-k] >= target))
        count++;
    }

    return count;
  }
};

int main()
{
  vector<int> input{1,1,1,1,1};
  Solution test;

  int res = test.numOfSubarrays(input, 1, 1);

  return 0;
}
```