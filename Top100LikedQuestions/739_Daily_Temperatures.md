# 739. Daily Temperatures

Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].

[LeetCode](https://leetcode.com/problems/daily-temperatures)

# 739. 每日溫度

請根據每日 氣溫 列表，重新生成一個列表。對應位置的輸出為：要想觀測到更高的氣溫，至少需要等待的天數。如果氣溫在這之後都不會升高，請在該位置用 0 來代替。

例如，給定一個列表 temperatures = [73, 74, 75, 71, 69, 72, 76, 73]，你的輸出應該是 [1, 1, 4, 2, 1, 1, 0, 0]。

提示：氣溫 列表長度的範圍是 [1, 30000]。每個氣溫的值的均為華氏度，都是在 [30, 100] 範圍內的整數


## Solution  
* stack

<img src="img/739.gif" width = "800"/>

### C++

* 時間複雜度 O(n)

* 空間複雜度 O(n)

```
#include <vector>
#include <stack>

using namespace std;

class Solution
{
public:
  vector<int> dailyTemperatures(vector<int> &temperatures)
  {
    stack<pair<int, int>> valuIdStack;

    int len = temperatures.size();
    vector<int> ret(len, 0);

    for (int i = 0; i < len; ++i)
    {

      while (valuIdStack.empty() != true && temperatures[i] > valuIdStack.top().first)
      {
        ret[valuIdStack.top().second] = i - valuIdStack.top().second;
        valuIdStack.pop();
      }

      valuIdStack.push(make_pair(temperatures[i], i));
    }

    return ret;
  }
};

int main()
{
  /* input*/
  vector<int> input = {30,40,50,60};

  /* test*/
  Solution test;
  vector<int> ret = test.dailyTemperatures(input);

  return 0;
}
```