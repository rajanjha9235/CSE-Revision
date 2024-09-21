# Knuth Moris Pratt Algorithm

- First we need to find the Longest Common Prefix and Suffix from beginning and ending for each element.
- For Example :- Pattern = `aabcaa` . LPS = [0 , 1 , 0 , 0 , 1 , 2] .
- For Example :- Pattern = `aaca` . LPS = [0 , 1 , 0 , 1] .
- `lps[i]` = Longest Proper prefix upto `pattern[i]` which is also suffix of `pattern[i]`
```python
def calculate_LPS(pattern : str) -> list[int]:
    size = len(pattern)
    lps = [0]*size
    lps[0] = 0  # As there is no prefix & suffix of length 1

    i = 1
    length = 0  # Length of previous lonest prefix & suffix

    while i < size:
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length > 0:
                length = lps[length-1]  # We can also do length -= 1
            else:
                lps[i] = 0
                i += 1  # Check further
    return lps
```
KMP Algorithm
```python
def KMP_algo(text : str , pattern : str):
    n = len(text)
    m = len(pattern)
    ans = []  # Store the indexes where this pattern found in text
    
    lps = compute_LPS(pattern)  # Find Lonest Common Prefix and Suffix for each element
    i = 0  #  Pointer of text
    j = 0  # Pointer of pattern
    while i < n:
        if text[i] == pattern[j]:  # Continue
            i += 1
            j += 1
        else:
            if j > 0:  # Send j to lps of (j-1)
                j = lps[j-1]
            else:  # j is at 0 already start matching from next i
                i += 1
        
        if j == m:  # We have found the pattern --> We can also return True
            ans.append(i-m)  # j is out of bound
            j = lps[j-1]
    
    return ans
```
- **Time Complexity** :- $$O(n + m)$$
- **Space Complexity** :- $$O(m)$$   where `m` is length of pattern
### Some Practice Problems :
- [Search Pattern GFG](https://www.geeksforgeeks.org/problems/search-pattern0205/1)

### [YouTube Video Solution](https://youtu.be/qases-9gOpk?si=MqYWopU67gSJo9Cl)
