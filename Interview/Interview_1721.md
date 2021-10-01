# 面試金典 1721 直方圖的水量

給定一個直方圖(也稱柱狀圖)，假設有人從上面源源不斷地倒水，最後直方圖能存多少水量?直方圖的寬度為 1

<img src="img/1721.png" width = "600"/>

## Volume of Histogram

Imagine a histogram (bar graph). Design an algorithm to compute the volume of water it could hold if someone poured water across the top. You can assume that each histogram bar has width 1.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/volume-of-histogram-lcci
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


[LeetCode](https://leetcode-cn.com/problems/volume-of-histogram-lcci)

### Example 1
```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

### C++ 

* 時間複雜度: O(n): 因為每個值只進出棧一次

```
#include <vector>
#include <stack>

using namespace std;

class Solution
{
public:
    int trap(vector<int> &height)
    {
        int len = height.size();
        if (len <= 2)
            return 0;

        stack<pair<int, int>> valStack;
        int volume = 0;
        for (int i = 0; i < len; ++i)
        {
            static int diff = 0;
            static int dist = 0;

            while (valStack.empty() != true && height[i] >= valStack.top().first)
            {
                pair<int, int> temp = valStack.top();
                valStack.pop();

                if(valStack.empty() == true)
                    break;
                diff = min(height[i], valStack.top().first) - temp.first;
                dist =  i - valStack.top().second - 1;

                volume += diff * dist;
            }

            valStack.push(make_pair(height[i], i));
        }

        return volume;
    }
};

int main(void)
{
    /* input*/
    vector<int> input = {0,1,0,2,1,0,1,3,2,1,2,1};

    /* Output*/
    Solution test;
    int res = test.trap(input);

    return 0;
}

```
