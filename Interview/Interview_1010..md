# 面試金典 1010 數字流的秩

假設你正在讀取一串整數。每隔一段時間，你希望能找出數字 x 的秩(小於或等於 x 的值的個數)。請實現數據結構和算法來支持這些操作，也就是說：

實現 track(int x) 方法，每讀入一個數字都會調用該方法；

實現 getRankOfNumber(int x) 方法，返回小於或等於 x 的值的個數。

##  Rank from Stream

Imagine you are reading in a stream of integers. Periodically, you wish to be able to look up the rank of a number x (the number of values less than or equal to x).
lmplement the data structures and algorithms to support these operations. That is, implement the method track (int x), which is called when each number is generated, and the method getRankOfNumber(int x), which returns the number of values less than or equal to x.

[LeetCode](https://leetcode-cn.com/problems/rank-from-stream-lcci/)

### Example 1
```
Input:
["StreamRank", "getRankOfNumber", "track", "getRankOfNumber"]
[[], [1], [0], [0]]
Output:
[null,0,null,1]
```

### C++ 

```
class StreamRank {
private:
    int len{0};
    vector<int> list;

    int binarySearch(int x)
    {
        int left = 0;
        int right = len - 1;
        int mid = 0;

        while (left < right)
        {
            mid = left + ((right - left) >> 1);
            if(list[mid] <= x)
                left = mid + 1;
            else    
                right = mid;
        }
        return left;
    }

public:
    StreamRank() {};
    
    void track(int x) {

        if( len == 0 || x >= list.back()){
            list.push_back(x);
        }
        else{
            int id = binarySearch(x);
            list.insert(list.begin() + id, x);
        }
        len++;
    }
    
    int getRankOfNumber(int x) {
        if( len == 0 || x >= list.back())
            return len;

        int id = binarySearch(x);

        return id;
    }
};
```
