### Notes

A `Trie` is a set of connected `TrieNode`s. The root node has no letter. A `Trie` that contains the words "food", "fox", and "he" is shown below

```
          ROOT
          /  \
         f    h
        /      \
       o        e
      / \
     o   x
    /
   d
```

One minor trick in creating a `Trie` is to omit storing any letters in the `TrieNode`s. Instead, the connections between `TrieNode`s will represent the letters, as shown in the pictures in [LeetCode's excellent official solution](https://leetcode.com/problems/implement-trie-prefix-tree/solution/) under "Insertion of a key to a trie"

### Solution

```java
class TrieNode {
    private Map<Character, TrieNode> children = new HashMap();
    public boolean isEnd = false; // "public" for simplicity

    public void putChildIfAbsent(char ch) {
        children.putIfAbsent(ch, new TrieNode());
    }

    public TrieNode getChild(char ch) {
        return children.get(ch);
    }
}
```

```java
class Trie {
    TrieNode root = new TrieNode();

    public void insert(String word) {
        TrieNode curr = root;
        for (char ch : word.toCharArray()) {
            curr.putChildIfAbsent(ch);
            curr = curr.getChild(ch);
        }
        curr.isEnd = true;
    }

    public boolean search(String word) {
        TrieNode curr = root;
        for (char ch : word.toCharArray()) {
            curr = curr.getChild(ch);
            if (curr == null) {
                return false;
            }
        }
        return curr.isEnd;
    }

    public boolean startsWith(String prefix) {
        TrieNode curr = root;
        for (char ch : prefix.toCharArray()) {
            curr = curr.getChild(ch);
            if (curr == null) {
                return false;
            }
        }
        return true;
    }
}

```
### Advantages over Hash Table approach

Although hash table has O(1) time complexity for looking for a key, it is not efficient in the following operations :

Finding all keys with a common prefix.
Enumerating a dataset of strings in lexicographical order

trie outperforms hash table, is that as hash table increases in size, there are lots of hash collisions and the search time complexity could deteriorate to O(n), where nn is the number of keys inserted. Trie could use less space compared to Hash Table when storing many keys with the same prefix. In this case using trie has only O(m)O(m) time complexity, where mm is the key length. Searching for a key in a balanced tree costs O(mlogn) time complexity.

### Time Complexity

- insert(): O(n)
- search(): O(n)
- startsWith(): O(n)

### Space Complexity

- insert(): O(n)
- search(): O(1)
- startsWith(): O(1)

### Other Applications of Trie

1. Finding all words (or the number of words) with a common prefix.
1. Enumerating a dataset of strings in alphabetical order.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/implement-trie-prefix-tree/discuss/343170)
- [github.com/RodneyShag](https://github.com/RodneyShag)
