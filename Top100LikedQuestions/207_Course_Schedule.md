# 207. Course Schedule
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

[LeetCode](https://leetcode.com/problems/course-schedule/)

### Example 1:
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

### Example 2:
```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

# 課程表
你這個學期必須選修 numCourses 門課程，記為 0 到 numCourses - 1 。

在選修某些課程之前需要一些先修課程。 先修課程按數組 prerequisites 給出，其中 prerequisites[i] = [ai, bi] ，表示如果要學習課程 ai 則 必須 先學習課程  bi 。

例如，先修課程對 [0, 1] 表示：想要學習課程 0 ，你需要先完成課程 1 。
請你判斷是否可能完成所有課程的學習？如果可以，返回 true ；否則，返回 false 。


## Solution  
* Breadth-First Search
<img src="img/207.gif" width = "1200/>

### C

```
#include <vector>
#include <queue>

using std::queue;
using std::vector;

class Solution
{
public:
  bool canFinish(int numCourses, vector<vector<int>> &prerequisites)
  {
    int reqLen = prerequisites.size();
    /**
     * TODO: count prerequisites value of each course
     *       store the link 
     * */
    vector<int> inDegree(numCourses);
    vector<vector<int>> link(numCourses);
    for (auto row : prerequisites)
    {
      ++inDegree[row[0]];
      link[row[1]].emplace_back(row[0]);
    }

    /**
     * TODO: Put the course whose prerequisite value is 0 into queue 
     * */
    queue<int> frontier;
    for (int i = 0; i < numCourses; ++i)
    {
      if (inDegree[i] == 0)
        frontier.push(i);
    }

    /**
     * TODO: Process the unit in the frontier, when a prerequisite unit is processed,
     *       its corresponding course inDegree minus 1, and the reqLen--   
     * */
    while (frontier.empty() != true)
    {
      int tmp = frontier.front();
      frontier.pop();
      for (auto course : link[tmp])
      {
        --inDegree[course];
        --reqLen;
        if (inDegree[course] == 0)
          frontier.push(course);
      }
    }

    return reqLen == 0;
  }
};

int main()
{
  int numCourses = 2;
  vector<vector<int>> prerequisites = {{1, 0}, {0, 1}};

  Solution test;
  bool ans = test.canFinish(numCourses, prerequisites);

  return 0;
}
```


