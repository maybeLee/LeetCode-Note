## 208 Implement Trie (Prefix Tree)

### *Description*

```
Implement a trie with insert, search, and startsWith methods.

Example:

Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
Note:

You may assume that all inputs are consist of lowercase letters a-z.
All inputs are guaranteed to be non-empty strings.
```



Trie里面的表达用list？



### *My Solution I: Python*

直接用list的基本操作方法就好....

#### *Code*

```python
class Trie(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.list = [];

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: None
        """
        self.list.append(word)
        

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        return word in self.list
        

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        length = len(prefix);
        for i in self.list:
            if len(i) >= length and i[:length] == prefix:
                return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```



#### *Result*

Runtime: 1088 ms, faster than 6.46% of Python online submissions for Implement Trie (Prefix Tree).

Memory Usage: 19.6 MB, less than 100.00% of Python online submissions for Implement Trie (Prefix Tree).

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313844145/) | 1092 ms | 19.5 MB | python   |
| a minute ago      | [Accepted](https://leetcode.com/submissions/detail/313843952/) | 1088 ms | 19.6 MB | python   |



### *My Solution II: Java*

Java 我用的不熟......主要是数组的一些用法不熟

From LeetCode

这道题原来很复杂啊.......

这道题其实是介绍了一个新的数据结构：Trie, Trie的功能：

- 在数据集中快速找到指定字符串
- 通过字符串前缀快速找到符合前缀的字符串

与HashTable的比较：

- HashTable也能在数据集中快速找到一个key （O(1) time complexity）。
- 不能根据前缀找到满足条件的所有key
- 不能将数据集的字符串按照字母的顺序遍历。

关于Trie, HashTable, Balanced Tree三种数据结构中搜寻字符串的效率比较：

|                 | Trie               | HashTable          | Balanced Tree |
| --------------- | ------------------ | ------------------ | ------------- |
| Time Complexity | O(m), m是key的长度 | O(n), n是key的数量 | O(mlogn)      |
| Extra Space     |                    |                    |               |



具体数据结构实现方法请见：https://leetcode.com/articles/implement-trie-prefix-tree/

比较核心的是构造了一个TrieNode类

Java中Final的用法：https://www.cnblogs.com/dolphin0520/p/3736238.html

```java
public class TrieNode {

    // R links to node children
    private TrieNode[] links;

    private final int R = 26;

    private boolean isEnd;

    public TrieNode() {
        links = new TrieNode[R];
    }

    public boolean containsKey(char ch) {
        return links[ch -'a'] != null;
    }
    public TrieNode get(char ch) {
        return links[ch -'a'];
    }
    public void put(char ch, TrieNode node) {
        links[ch -'a'] = node;
    }
    public void setEnd() {
        isEnd = true;
    }
    public boolean isEnd() {
        return isEnd;
    }
}

class Trie {

    /** Initialize your data structure here. */    
    private TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        
        for(int i = 0; i < word.length(); i++){
            char currentChar = word.charAt(i);
            if(!node.containsKey(currentChar)){
                node.put(currentChar, new TrieNode());
            }
            node = node.get(currentChar);
        }
        
        node.setEnd();
        
    }
    
    // search a prefix or whole key in trie and
    // returns the node where search ends
    private TrieNode searchPrefix(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
           char curLetter = word.charAt(i);
           if (node.containsKey(curLetter)) {
               node = node.get(curLetter);
           } else {
               return null;
           }
        }
        return node;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode node = searchPrefix(word);
        return node != null && node.isEnd();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode node = searchPrefix(prefix);
        return node != null;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```



Runtime: 31 ms, faster than 93.08% of Java online submissions for Implement Trie (Prefix Tree).

Memory Usage: 54.3 MB, less than 32.69% of Java online submissions for Implement Trie (Prefix Tree).

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313863694/) | 31 ms   | 54.3 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/313863654/) | 32 ms   | 54.4 MB | java     |