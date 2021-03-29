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
 

進階：你是否可以在 O(1) 時間覆雜度內完成這兩種操作？

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
    int key;
    int value;
    Node *prev;
    Node *next;
    Node() : key(0), value(0), prev(nullptr), next(nullptr){};
    Node(int _key, int _value) : key(_key), value(_value), prev(nullptr), next(nullptr){};
};

class LRUCache
{
private:
    int _capacity;
    int _size;
    Node *_head;
    Node *_tail;
    unordered_map<int, Node *> _map;

public:
    LRUCache(int capacity) : _capacity(capacity), _size(0)
    {
        _head = new Node();
        _tail = new Node();
        _head->next = _tail;
        _tail->prev = _head;
    }

    int get(int key)
    {
        if (_map.count(key) == 0)
            return -1;

        /** TODO: move it to the head*/
        Node *tmp = _map[key];
        moveToHead(tmp);

        return tmp->value;
    }

    void put(int key, int value)
    {
        if (_map.count(key) == 0)
        {
            /** TODO: creat new node*/
            Node *tmp = new Node(key, value);
            _map[key] = tmp;
            /** TODO: insert it to head */
            insertNode(tmp);
            ++_size;
            /** TODO: check if the size > capacity*/
            if (_size > _capacity)
            {
                /** TODO: remove the last node */
                removeLastNode();
                --_size;
            }
        }
        else
        {
            Node *tmp = _map[key];
            tmp->value = value;
            /** TODO: move it to the head*/
            moveToHead(tmp);
        }
    }

    void insertNode(Node *node)
    {
        node->next = _head->next;
        node->prev = _head;
        _head->next = node;
        node->next->prev = node;
    }

    void moveToHead(Node *node)
    {
        /* remove that node from current position*/
        node->prev->next = node->next;
        node->next->prev = node->prev;
        /* insert it to head */
        insertNode(node);
    }

    void removeLastNode()
    {
        Node *last = _tail->prev;
        _tail->prev = last->prev;
        _tail->prev->next = _tail;
        _map.erase(last->key);
        delete last;
    }
};

int main()
{
    LRUCache *obj = new LRUCache(2);
    obj->put(1, 1);
    obj->put(2, 2);
    obj->put(3, 3);
    int ans = obj->get(2);

    return 0;
}
```