# Sliding Window Algorithm
The Sliding Window algorithm is a powerful technique used primarily for solving problems that involve sequences, such as arrays or strings. It is particularly useful when you need to find contiguous subarrays or substrings that meet certain criteria.

![image](https://miro.medium.com/v2/resize:fit:1400/1*VXpfgmKhO0gNdgCoypJ41Q.gif)
### Key Concepts
1. **Window** : A range of elements within the array or string.
2. **Pointers** : Typically, two pointers (or indices) are used to define the boundaries of the window. These are often referred to as the left and right pointers.
3. **Dynamic Adjustment** : The window can grow or shrink by moving the pointers based on specific conditions defined in the problem.

### How It Works
1. **Initialization** : Start with both pointers at the beginning of the array or string.
2. **Expand the Window** : Move the right pointer to include more elements in the window until a certain condition is met (like reaching a target sum).
3. **Contract the Window** : Move the left pointer to reduce the window size when the condition is violated (like exceeding a target sum).
4. **Record Results** : Throughout this process, you can calculate and store results as needed.

![image](https://miro.medium.com/v2/resize:fit:1400/1*lcfE6u6wcUj7qxVY34Zidw.gif)

### Basic Template
- You have given a `target` and have to find a sub-array whose sum is target.
```python
nums = [4,6,3,8,9,32,53,1,12,70]
target = x   # Given Some target

n = len(nums)
i = 0  # Left pointer of window
j = 0   # Right Pointer of window
total = 0   # Sum of window

while j < n:
    total += nums[j]
    while total > target:  # Reduce the size of window as it exceeds the limit
        total -= nums[i]
        i += 1
    if total == target:   # If we got the answer either store it or return 
        ans = (i,j)
return ans
```

## Practice Problems :
- GFG : [Smallest window in a string containing all the characters of another string](https://www.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string-1587115621/1)

### Time Complexity :
The Sliding Window algorithm generally has a time complexity of $$O(n)$$, where n is the length of the array or string, since each element is processed at most twice (once added and once removed).

### Conclusion :
The Sliding Window technique is versatile and can be applied to a wide range of problems involving sequences. By choosing the appropriate type of sliding window, you can efficiently solve complex problems that would otherwise require more time-consuming approaches.
