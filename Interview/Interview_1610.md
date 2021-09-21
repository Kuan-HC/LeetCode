# 面試金典 1610 生存人數

給定 N 個人的出生年份和死亡年份，第 i 個人的出生年份為 birth[i]，死亡年份為 death[i]，實現一個方法以計算生存人數最多的年份。

你可以假設所有人都出生於 1900 年至 2000 年（含 1900 和 2000 ）之間。如果一個人在某一年的任意時期處於生存狀態，那麽他應該被納入那一年的統計中。
例如，生於 1908 年、死於 1909 年的人應當被列入 1908 年和 1909 年的計數。

如果有多個年份生存人數相同且均為最大值，輸出其中最小的年份。
 
##  Living People

Given a list of people with their birth and death years, implement a method to compute the year with the most number of people alive.
You may assume that all people were born between 1900 and 2000 (inclusive). If a person was alive during any portion of that year, 
they should be included in that year's count. 

For example, Person (birth= 1908, death= 1909) is included in the counts for both 1908 and 1909.

If there are more than one years that have the most number of people alive, return the smallest one.

[LeetCode](https://leetcode-cn.com/problems/living-people-lcci/)

### Example 1
```
Input: 
birth = {1900, 1901, 1950}
death = {1948, 1951, 2000}
Output:  1901
```


### C++ 

* 時間複雜度 O(n) 

* 空間複雜度 O(1): 不論input長度，皆需建立一prefix 的vector

```
class Solution
{
public:
    int maxAliveYear(vector<int> &birth, vector<int> &death)
    {
        vector<int> prefix(102, 0); // from year 1900 - 2000, but 2001 are take into account

        int len = birth.size();
        for (int i = 0; i < len; ++i)
        {
            prefix[birth[i] - 1900] += 1;
            prefix[death[i] + 1 - 1900] -= 1;
        }

        int maxNum = prefix[0];
        int year = 0;
        for (int i = 1; i < 102; ++i)
        {
            prefix[i] += prefix[i - 1];
            if(prefix[i] > maxNum)
            {
                maxNum = prefix[i];
                year = i;
            }
        }

        return year + 1900;
    }
};
```
