# 146. LRU Cache
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:

LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
int get(int key) Return the value of the key if the key exists, otherwise return -1.
void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
Follow up:
Could you do get and put in O(1) time complexity?

[LeetCode](https://leetcode.com/problems/lru-cache)  

### Example 1:

```
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4

```


# LRU 緩存機制

運用你所掌握的數據結構，設計和實現一個  LRU (最近最少使用) 緩存機制 。
實現 LRUCache 類：

LRUCache(int capacity) 以正整數作為容量 capacity 初始化 LRU 緩存
int get(int key) 如果關鍵字 key 存在於緩存中，則返回關鍵字的值，否則返回 -1 。
void put(int key, int value) 如果關鍵字已經存在，則變更其數據值；如果關鍵字不存在，則插入該組「關鍵字-值」。當緩存容量達到上限時，它應該在寫入新數據之前刪除最久未使用的數據值，從而為新的數據值留出空間。
 

進階：你是否可以在 O(1) 時間複雜度內完成這兩種操作？

## Solution

### C++

* Hash Table
```
#include <unordered_map>

using std::unordered_map;

/**
 * Definition for singly-linked list.
 * */

struct Node
{
    int key{0};
    int value{0};
    Node *prev{nullptr};
    Node *next{nullptr};
    Node(){};
    Node(int x, int y) : key(x), value(y){};
};

class LRUCache
{
public:
    int volumeMax{0};
    int volume{0};
    Node *start{nullptr};
    Node *tail{nullptr};
    unordered_map<int, Node *> keyMap;

public:
    LRUCache(int capacity) : volumeMax(capacity)
    {
        start = new Node(-1, -1);
        tail = start;
    }

    int get(int key)
    {
        if (keyMap.find(key) == keyMap.end())
            return -1;
        int ret = keyMap[key]->value;

        Node *temp = keyMap[key];
        //Node *temp = nullptr;

        if (temp != tail)
        {
            //remove it from current node and add to tail
            temp->prev->next = temp->next;
            temp->next->prev = temp->prev;
            tail->next = temp;
            temp->prev = tail;
            temp->next = nullptr;
            tail = tail->next;
        }

        return ret;
    }

    void put(int key, int value)
    {
        if (keyMap.find(key) != keyMap.end())
        { // this key already in the chain
            keyMap[key]->value = value;
            (void) get(key);
            return;
        }

        volume++;
        Node *temp = new Node(key, value);
        keyMap[key] = temp;
        // add it to the tail*/
        tail->next = temp;
        temp->prev = tail;
        tail = tail->next;

        if (volume > volumeMax)
        {
            //remove first node;
            temp = start->next;
            start->next = start->next->next;
            start->next->prev = start;
            keyMap.erase(temp->key);
            delete temp;
            volume--;
        }
    }
};
```