# 056. Merge Intervals

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

##  合併區間
給出一個區間的集合，請合併所有重疊的區間

[LeetCode](https://leetcode.com/problems/merge-intervals)  

### Example 1:

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

### Example 2:
```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping
```

## Solution

### C++

* 時間複雜度 排序 O(n log n) + 遍曆排序後的list O(n) 

* 空間複雜度 O (n)


```
class Solution
{
private:
  enum bracket
  {
    LEFT,
    RIGHT
  };

static bool comp( pair<int, bracket> &left, pair<int, bracket> &right)
{
    if(left.first == right.first)
      return left.second < right.second;

    return left < right;

}

public:
  vector<vector<int>> merge(vector<vector<int>> &intervals)
  {
    int len = intervals.size();
    if (len == 1)
      return intervals;

    vector<vector<int>> ret;
    /* store element as bracket in a vector*/
    vector<pair<int, bracket>> bracketList;

    for (int i = 0; i < len; ++i)
    {
      bracketList.emplace_back(make_pair(intervals[i][0], LEFT));
      bracketList.emplace_back(make_pair(intervals[i][1], RIGHT));
    }

    sort(bracketList.begin(), bracketList.end(), comp);

    /* use stack to remove bracket */
    stack<pair<int, bracket>> bracketStack;

    for (int i = 0; i < 2 * len; ++i)
    {
      if (bracketStack.empty() == true)
      {
        bracketStack.push(bracketList[i]);
        continue;
      }

      if (bracketStack.top().second == LEFT && bracketList[i].second == RIGHT)
      {
        if (bracketStack.size() == 1)
        {
          ret.push_back(vector<int>{bracketStack.top().first, bracketList[i].first});
        }
        bracketStack.pop();
      }
      else
        bracketStack.push(bracketList[i]);
    }

    return ret;
  }
};
```

### C

```
int comp(const void *a, const void *b)
{
    return (**(int **)a - **(int **)b);
}

void wrtie(int *tmpInterval, int *left, int *right, int *returnSize, int **retArray, int **intervals, const int index)
{
    if (*tmpInterval == true)
    {
        int *tmp = (int *)malloc(2 * sizeof(int));
        tmp[0] = *left;
        tmp[1] = *right;
        retArray[*returnSize] = tmp;
        *tmpInterval = false;
    }
    else
    {
        retArray[*returnSize] = intervals[index];
    }
    ++*returnSize;
}

int **merge(int **intervals, int intervalsSize, int *intervalsColSize, int *returnSize, int **returnColumnSizes)
{
    *returnSize = 0;
    /* sort intervals */
    qsort(intervals, intervalsSize, sizeof(int *), comp);

    /* space for storing result */
    int **retArray = (int **)malloc(sizeof(int *) * intervalsSize);

    int tmpInterval = false;
    int tmpRight = 0;
    int tmpLeft = 0;
    /* check interval*/
    int i = 0;
    for (i = 0; i < intervalsSize - 1; ++i)
    {
        if (tmpInterval == false)
        {
            tmpRight = intervals[i][1];
            tmpLeft = intervals[i][0];
        }

        if (tmpRight >= intervals[i + 1][0])
        {
            tmpInterval = true;
            tmpRight = tmpRight > intervals[i + 1][1] ? tmpRight : intervals[i + 1][1];
        }
        else
            wrtie(&tmpInterval, &tmpLeft, &tmpRight, returnSize, retArray, intervals, i);
    }
    /* process last element */
    wrtie(&tmpInterval, &tmpLeft, &tmpRight, returnSize, retArray, intervals, intervalsSize - 1);

    *returnColumnSizes = (int *)malloc(sizeof(int) * (*returnSize));
    for (i = 0; i < (*returnSize); ++i)
        (*returnColumnSizes)[i] = 2;

    return retArray;
}

int main()
{
    int a[2] = {2, 3};
    int b[2] = {4, 5};
    int c[2] = {6, 7};
    int d[2] = {8, 9};
    int e[2] = {1, 10};
    int size = 5;
    int **input = (int **)malloc(sizeof(int *) * size);

    input[0] = b;
    input[1] = a;
    input[2] = c;
    input[3] = d;
    input[4] = e;

    int intervalsColSize = 2;
    int returnSize = 0;
    int **returnColumnSizes = (int **)malloc(sizeof(int *));

    int **ans = merge(input, size, &intervalsColSize, &returnSize, returnColumnSizes);

    for (int i = 0; i < returnSize; ++i)
    {
        printf("[%d, %d] ", ans[i][0], ans[i][1]);
    }

    return 0;
}
```
