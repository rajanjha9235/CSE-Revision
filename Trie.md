# Trie Data Structure

A Trie, or prefix tree, is a specialized tree-like data structure used primarily for storing strings in a way that facilitates efficient retrieval, especially for prefix searches. Here are some key features and concepts associated with Tries:

#### Structure :-
- **Nodes** : Each node represents a single character of a string.
- **Root Node** : The starting point of the Trie, usually an empty node.
- **Children** : Each node can have multiple children, representing possible continuations of the string.
- **End of Word Marker** : Nodes may contain a flag to indicate whether they represent the end of a valid string.

![image](https://datastructures.maximal.io/img/tries/trie-1.svg)
#### Characteristics :
- **Efficiency** : Tries enable fast insertions, deletions, and lookups, typically with a time complexity of O(m), where m is the length of the string.
- **Prefix Search** : They excel in scenarios where prefix searches are common, making them suitable for applications like autocomplete and spell checking.
- **Memory Usage** : Tries can use more memory than other data structures due to the overhead of storing pointers for each character.
![image](https://miro.medium.com/v2/resize:fit:1396/1*e3549k5A9oCLn-vZTxsFEA.gif)
#### Operations:
- **Insert** : Adding a string involves traversing the Trie, creating new nodes as needed.
- **Search** : Checking for a string's presence or finding all strings with a given prefix.
- **Delete** : Removing a string involves traversing to the end of the string and marking it as not a valid word, then cleaning up any nodes that are no longer needed.
![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*aJxRGNYe52CE_bVRt0E1Eg.gif)



### Trie Node
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False
```

### Insertion :
```python
def insert(word : str) -> None:
    curr = root
    for char in word:
        if char not in curr.children:  # Not Present in Children
            curr.children[char] = TrieNode()  # Add a new Node
        curr = curr.children[char]
    curr.is_word = True  # Mark it as a word
```

### Searching :
```python
def search(word : str) -> bool:
    curr = root
    for char in word:
        if char not in curr.children:  # Means  it's not present
            return False
        curr = curr.children[char]

    # We have reached upto the last character but it's not necessary that it's a word --> It can also be a part of another word
    if curr.is_word == True:  
        return True
    return False
```
### Starts With :
```python
def starts_with(prefix : str) -> bool:
    curr = root
    for char in word:
        if char not in curr.children:  # Means  it's not present
            return False
        curr = curr.children[char]
    return True  # This prefix is present in Trie
```
## Implementing Trie
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end = False

class Trie:

    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        curr = self.root
        for char in word:
            if char not in curr.children:  # Not Present in children
                curr.children[char] = TrieNode()   # Add a new node
            curr = curr.children[char]
        curr.end = True  # Mark it a word

    def search(self, word: str) -> bool:
        curr = self.root
        for char in word:
            if char not in curr.children:
                return False
            curr = curr.children[char]

        # We have reached upto the last character but it's not necessary that it's a word --> It can also be a part of another word
        if curr.end == True:
            return True
        return False

    def startsWith(self, prefix: str) -> bool:
        curr = self.root
        for char in prefix:
            if char not in curr.children:  # # Means  it's not present
                return False
            curr = curr.children[char]
        return True     # This prefix is present in Trie
```

![image](https://hackernoon.com/hn-images/1*X1t7eWTWF0u8IcDkvDrxdA.gif)

## Time Complexity :
The time complexity of operations in a Trie largely depends on the length of the strings involved rather than the number of strings stored. Here are the complexities for the primary operations:

1. **Insertion**
   - Time Complexity : $$O(m)$$
   - Where m is the length of the string being inserted. Each character in the string is processed, resulting in a linear time complexity relative to the string's length.

3. **Search**
    - Time Complexity: O(m)
    - Similar to insertion, searching for a string also involves traversing each character of the string, leading to a linear time complexity based on the string's length.

4. **Deletion**
    - Time Complexity: O(m)
    - Deleting a string involves traversing the Trie to find the end of the string, and potentially modifying the structure to remove nodes that are no longer needed. This also takes linear time relative to the length of the string.

5. **Prefix Search**
   - Time Complexity: O(m)
   - Searching for all strings with a given prefix involves traversing the Trie up to the length of the prefix, which is also linear in terms of the prefix length.

6. **Listing All Words**
   - Time Complexity: O(m * n)
   - If you want to list all words stored in the Trie, where n is the number of words, the time complexity can be considered O(m * n) because you might need to traverse each word stored, and each traversal is O(m).

- In summary, the key takeaway is that the operations of inserting, searching, and deleting strings in a Trie have a time complexity of O(m), where m is the length of the string involved. This makes Tries efficient for handling string operations, especially when dealing with a large number of strings or prefix-based queries.

## Practice Problems :
1. **LeetCode 208** : [Trie Implementation](https://leetcode.com/problems/implement-trie-prefix-tree/)
2. **LeetCode 3043** : [Find Length of Longest Common Prefix](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/)
3. **LeetCode 2416** :  [Sum of Prefix scores of Strings](https://leetcode.com/problems/sum-of-prefix-scores-of-strings)

#### Applications:
- Autocomplete systems
- Spell checkers
- IP routing
- Dictionary implementations

Overall, Tries are a powerful tool for handling dynamic sets of strings and performing various string-related operations efficiently.
