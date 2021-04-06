# 208. Implement Trie (Prefix Tree)
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

Trie() Initializes the trie object.
void insert(String word) Inserts the string word into the trie.
boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

[LeetCode](https://leetcode.com/problems/implement-trie-prefix-tree/)

### Example 1:
```
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```

# 實現 Trie (前缀樹)
Trie（发音類似 "try"）或者說 前綴樹 是一種樹形數據結構，用於高效地存儲和檢索字符串數據集中的鍵。這一數據結構有相當多的應用情景，例如自動補完和拼寫檢查。

請你實現 Trie 類：

*Trie() 初始化前綴樹對象。
*void insert(String word) 向前綴樹中插入字符串 word 。
*boolean search(String word) 如果字符串 word 在前綴樹中，返回 true（即，在檢索之前已經插入）；否則，返回 false 。
*boolean startsWith(String prefix) 如果之前已經插入的字符串 word 的前綴之一為 prefix ，返回 true ；否則，返回 false 。


## Solution  
[wiki](https://en.wikipedia.org/wiki/Trie)


### C

```
typedef struct Trie
{
  bool finished;
  struct Trie *next[26];
} Trie;

/** Initialize your data structure here. */

Trie *trieCreate()
{
  Trie *tmp = (Trie *)calloc(1, sizeof(struct Trie));

  return tmp;
}

// /** Inserts a word into the trie. */
void trieInsert(Trie *obj, char *word)
{
  int len = strlen(word);

  for (int i = 0; i < len; ++i)
  {
    int num = word[i] - 'a';
    if (obj->next[num] == NULL)
      obj->next[num] = (Trie *)calloc(1, sizeof(struct Trie));      
    
    obj = obj->next[num];
  }
  obj->finished = true;
}

// /** Returns if the word is in the trie. */
bool trieSearch(Trie *obj, char *word)
{
  int len = strlen(word);

  for (int i = 0; i < len; ++i)
  {
    int num = word[i] - 'a';
    if (obj->next[num] == NULL)
      return false;
    obj = obj->next[num];
  }
  return obj->finished == true;
}

// /** Returns if there is any word in the trie that starts with the given prefix. */
bool trieStartsWith(Trie *obj, char *prefix)
{
  int len = strlen(prefix);

  for (int i = 0; i < len; ++i)
  {
    int num = prefix[i] - 'a';
    if (obj->next[num] == NULL)
      return false;
    obj = obj->next[num];
  }
  return true;
}

void trieFree(Trie *obj)
{
  if (obj == NULL)
    return;

  for (int i = 0; i < 26; ++i)
  {
    if(obj->next[i] != NULL){
      obj = obj->next[i];
      trieFree(obj);
    }
  }
  free(obj);
}

int main()
{
  Trie *obj = trieCreate();

  char word_1[] = "apple";
  trieInsert(obj, word_1);

  
  bool param_2 = trieSearch(obj, word_1);

  char word_2[] = "app";
  bool param_3 = trieSearch(obj, word_2);

  bool param_4 = trieStartsWith(obj, word_2);

  trieInsert(obj, word_2);

  bool param_5 = trieSearch(obj, word_2);

  trieFree(obj);

  return 0;
}
```

### C++

```
#include <string>
using std::string;

class Trie
{
private:
  bool finished{false};
  Trie *next[26]{nullptr};

public:
  /** Initialize your data structure here. */
  Trie() {}

  /** Inserts a word into the trie. */
  void insert(string word)
  {
    Trie *root = this;
    int num = 0;
    for (const auto &letter : word)
    {
      num = letter - 'a';
      if (root->next[num] == nullptr)
        root->next[num] = new Trie();

      root = root->next[num];
    }
    root->finished = true;
  }

  /** Returns if the word is in the trie. */
  bool search(string word)
  {
    Trie *root = this;
    int num = 0;
    for (const auto &letter : word)
    {
      num = letter - 'a';
      if (root->next[num] == nullptr)
        return false;
      root = root->next[num];
    }
    return root->finished;
  }

  /** Returns if there is any word in the trie that starts with the given prefix. */
  bool startsWith(string prefix)
  {
    Trie *root = this;
    int num = 0;
    for (const auto &letter : prefix)
    {
      num = letter - 'a';
      if (root->next[num] == nullptr)
        return false;
      root = root->next[num];
    }
    return true;
  }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */

int main()
{
  Trie *obj = new Trie();
  obj->insert("apple");

  string word = "app";

  bool param_2 = obj->search(word);
  bool param_3 = obj->startsWith(word);

  return 0;
}
```
