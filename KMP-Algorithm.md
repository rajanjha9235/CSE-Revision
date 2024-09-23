# Knuth Moris Pratt Algorithm
The KMP (Knuth-Morris-Pratt) algorithm is an efficient method for searching for a substring within a main string. It improves the search process by avoiding unnecessary comparisons.
![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*lA9ysp9igTuUwsbPxI8VQQ.png)
![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Ixnj2k8qd9wxkTgKolhH0g.png)
### Key Features:
- **Preprocessing Phase** : KMP constructs a "longest prefix-suffix" (LPS) array for the pattern, which helps determine how far to jump in the pattern after a mismatch.
- **Search Phase** : It scans through the main string using the pattern, utilizing the LPS array to skip over portions of the pattern, reducing the number of comparisons needed.

![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*wgpZZqgzoJ706gzjPiaG1A.png)
![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*fYWz9Rdqfl11FFjQjfiMHg.png)

### How It Works:
- **Build the LPS Array** : For each position in the pattern, the LPS array indicates the length of the longest proper prefix which is also a suffix.
- ![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*R1-PCF78paVBRGBlJyx6uw.png)
- ![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*e5uz6qGt77btRVI4Dbj36w.png)
- ![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*mlEp0cOmChpE2asGpzoSeQ.png)
- ![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*LJbzImGYYj0jowL6gbdeLg.png)

- **Match the Strings** : Start matching the main string and the pattern. On a mismatch, use the LPS array to determine the next positions to compare, instead of starting over from the beginning of the pattern.
- 
- ![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*0isa_pKn3o77jOHiusvtew.png)
- ![image](https://miro.medium.com/v2/resize:fit:720/format:webp/1*cjdpNXCHc2LFne12YpKJPw.png)
- 
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
- Then we will search the Pattern inside the text given effectively with the help of `LPS`.
```python
def Search(text : str , pattern : str):
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


This algorithm is widely used in string processing tasks, including searching in text editors and implementing features like substring search in programming languages.

### Some Practice Problems :
- GFG : [Search Pattern](https://www.geeksforgeeks.org/problems/search-pattern0205/1)
- LeetCode 214 : [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/description/)
- GFG : [Longest Prefix Suffix](https://www.geeksforgeeks.org/problems/longest-prefix-suffix2527/1)

### [YouTube Video Solution](https://youtu.be/qases-9gOpk?si=MqYWopU67gSJo9Cl)
