# 1343. 和可被 K 整除的子數組

給定一個整數數組 A，返回其中元素之和可被 K 整除的（連續、非空）子數組的數目。

[LeetCode](https://leetcode-cn.com/problems/subarray-sums-divisible-by-k)

### Example 1:
```
輸入：A = [4,5,0,-2,-3,1], K = 5
輸出：7
解釋：
有 7 個子數組滿足其元素之和可被 K = 5 整除：
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
```
 
* 1 <= A.length <= 30000
* -10000 <= A[i] <= 10000
* 2 <= K <= 10000


## Solution  

### C++

* 時間複雜度：O(n)   需執行鍊表長度 + 1次  空間複雜度 n

* 空間複雜度：O(n)   需鍊表長度+1的空間

```
#include <vector>
#include <unordered_map>

using namespace std;

class Solution
{
public:
  int subarraysDivByK(vector<int> &nums, int k)
  {

    unordered_map<int, int> prefixRemainder;
    prefixRemainder[0] = 1; // initial setting: we have one "zero"

    int count = 0;
    int sum = 0;
    int target = 0;

    for (const auto &num : nums)
    {
      sum += num;
      target = ((sum % k) + k) % k;

      if (prefixRemainder.find(target) != prefixRemainder.end())
        count += prefixRemainder[target];

      prefixRemainder[target]++;
    }

    return count;
  }
};

int main()
{
  vector<int> input{4, 5, 0, -2, -3, 1};
  Solution test;

  int res = test.subarraysDivByK(input, 5);

  return 0;
}

```