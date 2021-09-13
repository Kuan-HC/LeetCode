# 面試金典 0306 動物收容所

動物收容所。有家動物收容所只收容狗與貓，且嚴格遵守“先進先出”的原則。在收養該收容所的動物時，收養人只能收養所有動物中“最老”（由其進入收容所的時間長短而定）的動物，或者可以挑選貓或狗（同時必須收養此類動物中“最老”的）。換言之，收養人不能自由挑選想收養的對象。請創建適用於這個系統的數據結構，實現各種操作方法，比如enqueue、dequeueAny、dequeueDog和dequeueCat。允許使用Java內置的LinkedList數據結構。

enqueue方法有一個animal參數，animal[0]代表動物編號，animal[1]代表動物種類，其中 0 代表貓，1 代表狗。

dequeue*方法返回一個列表[動物編號, 動物種類]，若沒有可以收養的動物，則返回[-1,-1]。


##  Animal Shelter
An animal shelter, which holds only dogs and cats, operates on a strictly"first in, first out" basis. People must adopt either the"oldest" (based on arrival time) of all animals at the shelter, or they can select whether they would prefer a dog or a cat (and will receive the oldest animal of that type). They cannot select which specific animal they would like. Create the data structures to maintain this system and implement operations such as enqueue, dequeueAny, dequeueDog, and dequeueCat. You may use the built-in Linked list data structure.

enqueue method has a animal parameter, animal[0] represents the number of the animal, animal[1] represents the type of the animal, 0 for cat and 1 for dog.

dequeue* method returns [animal number, animal type], if there's no animal that can be adopted, return [-1, -1].


[LeetCode](https://leetcode-cn.com/problems/animal-shelter-lcci)


### Example 1

```
Input: 
["AnimalShelf", "enqueue", "enqueue", "dequeueCat", "dequeueDog", "dequeueAny"]
[[], [[0, 0]], [[1, 0]], [], [], []]
 Output: 
[null,null,null,[0,0],[-1,-1],[1,0]]

```

### C++ 

```
#include <vector>
#include <string>
#include <queue>

using namespace std;

class AnimalShelf
{
private:
    queue<vector<int>> dog;
    queue<vector<int>> cat;

public:
    AnimalShelf()
    {
    }

    void enqueue(vector<int> animal)
    {
        if (animal[1] == 0)
            cat.emplace(animal);
        else
            dog.emplace(animal);
    }

    vector<int> dequeueAny()
    {

        if (dog.empty() == true && cat.empty() == true)
        {
            return vector<int> {-1, -1};
        }
        else if (dog.empty() == true)
        {
            return dequeueCat();
        }
        else if(cat.empty() == true)
        {
            return dequeueDog();
        }
        else
        {
            if(dog.front() < cat.front())
                return dequeueDog();
            else
                return dequeueCat();
        }
    }

    vector<int> dequeueDog()
    {
        vector<int> ret = {-1, -1};
        if (dog.empty() == true)
            return ret;

        ret = dog.front();
        dog.pop();

        return ret;
    }

    vector<int> dequeueCat()
    {
        vector<int> ret = {-1, -1};
        if (cat.empty() == true)
            return ret;

        ret = cat.front();
        cat.pop();

        return ret;
    }
};

int main()
{
    /* input */

    /* Algorithm */
    AnimalShelf *obj = new AnimalShelf();
    obj->enqueue(vector<int>{1, 0});
    obj->enqueue(vector<int>{0, 1});
    vector<int> param_1 = obj->dequeueDog();
    vector<int> param_2 = obj->dequeueDog();

    return 0;
}
```
