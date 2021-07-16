# 劍指 Offer 11 旋转数组的最小数字

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

[LeetCode](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

### Example 1
```
輸入：[3,4,5,1,2]
輸出：1
```

### Example 2
```
輸入：[2,2,2,0,1]
輸出：0
```

## Solution  

### C++

* 時間複雜度：o(log n)
* 空間複雜度：o(1)

```
#include <vector>

using namespace std;

class Solution
{
public:
    int minArray(vector<int> &numbers)
    {
        int len = numbers.size();
        if (len == 0)
            return 0;

        int left = 0;
        int right = len - 1;
        int mid = 0;

        while (left < right)
        {
            mid = left + (right - left) / 2;

            if (numbers[mid] > numbers[right])
                left = mid + 1;
            else if(numbers[mid] < numbers[right])
                right = mid ;
            else
                right--;
        }

int main()
{
    /* Input */
    vector<int> input = {2,2,2,0,1};

    /* Test*/
    Solution test;
    int res = test.minArray(input);

    return 0;
}
```
