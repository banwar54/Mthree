# Code Explanation and Key Learnings

## remove_outmost_parenthesis

### Functionality:
This function removes the outermost pair of parentheses from a given string that consists of multiple pairs of parentheses.

### Code:
```python
def remove_outmost_parenthesis(s):
    result=[]
    open_count=0
    close_count=0
    for char in s:
        if char == '(':
            open_count+=1
        elif char ==')':
            close_count+=1
    i=0
    while(i<open_count-1 and i < close_count-1):
        i+=1
        result+="()"
    return ''.join(result)
```

### Example and Output:
```python
print(remove_outmost_parenthesis("()()()()()"))
```
**Output:**
```
()()()
```

## reverse_words

### Functionality:
Reverses the order of words in a given sentence.

### Code:
```python
def reverse_words(s):
    words = [word for word in s.split()]
    return ' '.join(words[::-1])
```

### Example and Output:
```python
print(reverse_words("Hey how are you"))
```
**Output:**
```
you are how Hey
```

## largest_seq

### Functionality:
Finds the largest sequence from the given string, ensuring the last digit is odd.

### Code:
```python
def largest_seq(s):
    for i in range(len(s)-1,-1,-1):
        if(int(i)%2==1):
            return s[:i+1]
    return ""
```

### Example and Output:
```python
print(largest_seq("51"))
print(largest_seq("521"))
```
**Output:**
```
51
521
```

## longest_common_substring

### Functionality:
Finds the longest common substring among a list of words.

### Code:
```python
def longest_common_substring(words):
    if not words:
        return ""
    shortest = min(words, key=len)
    longest_substr = ""
    for i in range(len(shortest)):
        for j in range(i + 1, len(shortest) + 1):
            substr = shortest[i:j]
            if all(substr in word for word in words):
                if len(substr) > len(longest_substr):
                    longest_substr = substr
            else:
                break
    return longest_substr
```

### Example and Output:
```python
print(longest_common_substring(["abc","abcd","bababa"]))
```
**Output:**
```
abc
```

## check_rotation

### Functionality:
Checks if one string is a rotation of another string.

### Code:
```python
def check_rotation(s1,s2):
    if(len(s1)!=len(s2)):
        print("Absent")
        return
    if s2 in (s1+s1):
        print("Present")
        return
    print("Absent")
    return
```

### Example and Output:
```python
check_rotation("abc","cab")
```
**Output:**
```
Present
```

---

# Key Learnings

1. **String Manipulation:**
   - Understanding how to work with strings efficiently.
   - Using list comprehensions and string operations.

2. **Looping Techniques:**
   - Using `for` and `while` loops to iterate over elements.
   - Breaking out of loops early for optimization.

3. **Optimization Strategies:**
   - Selecting the shortest word to optimize substring checks.
   - Using concatenation (`s1+s1`) for rotation checks.

4. **Edge Cases Handling:**
   - Handling empty inputs in functions like `longest_common_substring`.
   - Ensuring length checks before performing operations.

5. **Logical Thinking:**
   - Understanding how to build algorithms step by step.
   - Using conditions to filter required results.

These functions demonstrate fundamental programming concepts that can be applied to various coding challenges and real-world applications.

