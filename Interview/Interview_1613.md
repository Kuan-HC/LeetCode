# 面試金典 1613 平分正方形

給定兩個正方形及一個二維平面。請找出將這兩個正方形分割成兩半的一條直線。假設正方形頂邊和底邊與 x 軸平行。

每個正方形的數據square包含3個數值，正方形的左下頂點坐標[X,Y] = [square[0],square[1]]，以及正方形的邊長square[2]。
所求直線穿過兩個正方形會形成4個交點，請返回4個交點形成線段的兩端點坐標（兩個端點即為4個交點中距離最遠的2個點，這2個點所連成的線段一定會穿過另外2個交點）。
2個端點坐標[X1,Y1]和[X2,Y2]的返回格式為{X1,Y1,X2,Y2}，要求若X1 != X2，需保證X1 < X2，否則需保證Y1 <= Y2。

若同時有多條直線滿足要求，則選擇斜率最大的一條計算並返回（與Y軸平行的直線視為斜率無窮大）。

 
[LeetCode](https://leetcode-cn.com/problems/bisect-squares-lcci/)

### Example 1
```
Input: 
square1 = {-1, -1, 2}
square2 = {0, -1, 2}
Output: {-1,0,2,0}
Explanation: y = 0 is the line that can cut these two squares in half.
```


### C++ 

* 時間複雜度 O(1) 

* 空間複雜度 O(1)

```
class Solution
{
private:
    double getX(pair<double, double> cent1, pair<double, double> cent2, double y)
    {
        return (y - cent1.second) / (cent2.second - cent1.second) * (cent2.first - cent1.first) + cent1.first;
    }

    double getY(pair<double, double> cent1, pair<double, double> cent2, double x)
    {
        return (x - cent1.first) / (cent2.first - cent1.first) * (cent2.second - cent1.second) + cent1.second;
    }

public:
    vector<double> cutSquares(vector<int> &square1, vector<int> &square2)
    {
        /* 中心點位置*/
        pair<double, double> cent1 = make_pair(square1[0] + (double)square1[2] / 2, square1[1] + (double)square1[2] / 2);
        pair<double, double> cent2 = make_pair(square2[0] + (double)square2[2] / 2, square2[1] + (double)square2[2] / 2);

        /*對上下左右各邊排序*/
        vector<int> verticalOrder = {square1[1], square1[1] + square1[2], square2[1], square2[1] + square2[2]};
        vector<int> horizontalOrder = {square1[0], square1[0] + square1[2], square2[0], square2[0] + square2[2]};

        sort(verticalOrder.begin(), verticalOrder.end());
        sort(horizontalOrder.begin(), horizontalOrder.end());

        /* 已知中心二點，求點斜式，對垂直及水平的情形單獨處理*/
        if (cent1.first == cent2.first) //垂直
            return vector<double>{cent1.first, (double)verticalOrder.front(), cent1.first, (double)verticalOrder.back()};
        if (cent1.second == cent2.second) //水平
            return vector<double>{(double)horizontalOrder.front(), cent1.second, (double)horizontalOrder.back(), cent1.second};

        // 連線的斜率
        double slope = fabs((cent2.second - cent1.second) / (cent2.first - cent1.first));
        // 斜率大於等於 1 ，接觸 上下邊，小於1左右邊
        if (slope >= 1.0) // y 已知，求x
        {
            double temp1 = getX(cent1, cent2, (double)verticalOrder.front());
            double temp2 = getX(cent1, cent2, (double)verticalOrder.back());
            if (temp1 < temp2)
                return vector<double>{temp1, (double)verticalOrder.front(), temp2, (double)verticalOrder.back()};
            else
                 return vector<double>{temp2, (double)verticalOrder.back(), temp1, (double)verticalOrder.front()};
        }
        else
        {
            double temp1 = getY(cent1, cent2, (double)horizontalOrder.front());
            double temp2 = getY(cent1, cent2, (double)horizontalOrder.back());
            return vector<double>{(double)horizontalOrder.front(), temp1, (double)horizontalOrder.back(), temp2};
        }
    }
};
```
