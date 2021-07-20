# 劍指 Offer 40 最小的k個數

輸入整數數組 arr ，找出其中最小的 k 個數。例如，輸入4、5、1、6、2、7、3、8這8個數字，則最小的4個數字是1、2、3、4。


[LeetCode](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

### Example 1


```
輸入：arr = [3,2,1], k = 2
輸出：[1,2] 或者 [2,1]
```

### Example 2

```
輸入：arr = [0,1,2,1], k = 1
輸出：[0]
```

* 0 <= k <= arr.length <= 10000
* 0 <= arr[i] <= 10000
 
## Solution  

### C++

* 時間複雜度：O(n) 其中n是鍊表的長度，需要遍曆鍊表一次。

* 空間複雜度：O(n) 哈希表空間

<img src="img/35.jpg" width = "500"/>


```
#include <vector>
#include <algorithm>

using namespace std;


class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k)
    {
        sort(arr.begin(), arr.end());

        vector<int> ret(arr.begin(), arr.begin()+k);

        return ret;               
        
    }
};

int main()
{
    /* input*/
    vector<int> input = {0,1,2,1};

    /* Test*/
    Solution test;
    vector<int> res = test.getLeastNumbers(input, 2);
    return 0;
}
```