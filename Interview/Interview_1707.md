# 面試金典 1707 嬰兒名字

每年，政府都會公布一萬個最常見的嬰兒名字和它們出現的頻率，也就是同名嬰兒的數量。有些名字有多種拼法，例如，John 和 Jon 本質上是相同的名字，但被當成了兩個名字公布出來。
給定兩個列表，一個是名字及對應的頻率，另一個是本質相同的名字對。設計一個算法打印出每個真實名字的實際頻率。
注意，如果 John 和 Jon 是相同的，並且 Jon 和 Johnny 相同，則 John 與 Johnny 也相同，即它們有傳遞和對稱性。

在結果列表中，選擇 字典序最小 的名字作為真實名字。

[LeetCode](https://leetcode-cn.com/problems/baby-names-lcci)

### Example 1
```
Input: names = ["John(15)","Jon(12)","Chris(13)","Kris(4)","Christopher(19)"], synonyms = ["(Jon,John)","(John,Johnny)","(Chris,Kris)","(Chris,Christopher)"]
Output: ["John(27)","Chris(36)"]

```

### C++ 


```
#include <vector>
#include <unordered_map>
#include <string>
#include <algorithm>

using namespace std;

class Solution
{
public:
    vector<string> trulyMostPopular(vector<string> &names, vector<string> &synonyms)
    {
        if (names.size() == 0)
            return {};

        vector<string> ret;
        /* create a relation between synonyms*/
        unordered_map<string, string> nameMap;
        for (const auto &name : synonyms)
        {
            int comma = name.find(",");
            int len = name.length();

            string first = name.substr(1, comma - 1);
            string second = name.substr(comma + 1, len - comma - 2);

            while (nameMap.find(first) != nameMap.end())
                first = nameMap[first];

            while (nameMap.find(second) != nameMap.end())
                second = nameMap[second];

            if (first != second)
            {
                if (first > second)
                    nameMap[first] = second;
                else
                    nameMap[second] = first;
            }
        }

        /* count names*/
        unordered_map<string, int> nameCounter;
        for (const auto &data : names)
        {
            int lBracket = data.find("(");

            string name = data.substr(0, lBracket);
            int val = stoi(data.substr(lBracket + 1, data.find(")") - lBracket - 1));

            while (nameMap.find(name) != nameMap.end())
                name = nameMap[name];

            nameCounter[name] += val;
        }

        /* transfer data into string for output*/
        for (const auto &item : nameCounter)
        {
            string temp = item.first;
            temp += "(" + to_string(item.second) + ")";
            ret.emplace_back(temp);
        }

        return ret;
    }
};

int main()
{
    /* input */
    vector<string> names = {"John(15)", "Jon(12)", "Chris(13)", "Kris(4)", "Christopher(19)"};
    vector<string> synonyms = {
        "(Uzgx,Siv)",
        "(Dwifi,Uzgx)",
        "(Uxf,Uzgx)",
        "(Jon,John)",
        "(John,Johnny)",
        "(Chris,Kris)",
        "(Chris,Christopher)",
    };

    /* Test */
    Solution test;
    vector<string> res = test.trulyMostPopular(names, synonyms);

    return 0;
}
```
