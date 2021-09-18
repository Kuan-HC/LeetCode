# 面試金典 1602 單詞頻率

設計一個方法，找出任意指定單詞在一本書中的出現頻率。

你的實現應該支持如下操作：

* WordsFrequency(book)構造函數，參數為字符串數組構成的一本書
* get(word)查詢指定單詞在書中出現的頻率
 
##  Words Frequency

Design a method to find the frequency of occurrences of any given word in a book. What if we were running this algorithm multiple times?

You should implement following methods:

* WordsFrequency(book) constructor, parameter is a array of strings, representing the book.
* get(word) get the frequency of word in the book. 

[LeetCode](https://leetcode-cn.com/problems/words-frequency-lcci/)


### Example 1

```
WordsFrequency wordsFrequency = new WordsFrequency({"i", "have", "an", "apple", "he", "have", "a", "pen"});
wordsFrequency.get("you"); //returns 0，"you" is not in the book
wordsFrequency.get("have"); //returns 2，"have" occurs twice in the book
wordsFrequency.get("an"); //returns 1
wordsFrequency.get("apple"); //returns 1
wordsFrequency.get("pen"); //returns 1

```

### C++ 

* 時間複雜度 O(n)

* 空間複雜度 O(n)

```
class WordsFrequency {
private:
    unordered_map<string, int>wordCounter;

public:
    WordsFrequency(vector<string>& book) {
        for(const string& word: book)
            wordCounter[word]++;
    }
    
    int get(string word) {
        return wordCounter[word];
    }
};
```
