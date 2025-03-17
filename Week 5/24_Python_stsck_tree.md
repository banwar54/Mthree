# Comprehensive Analysis of Data Structures

## 1. Stack Data Structure

A stack is a linear data structure that follows the **Last-In-First-Out (LIFO)** principle. This means that the last element added to the stack will be the first one to be removed. The analogy often used is a stack of plates: you can only take the top plate, and you can only add a new plate to the top.

### 1.1 Stack Implementation:

This implementation provides a feature-rich stack with support for various Python operations:

```python
class Stack:
    def __init__(self):
        self.items = []  # Using a list as the underlying data structure
```

#### 1.1.1 Core Stack Operations:

- **`is_empty()`**: 
  ```python
  def is_empty(self):
      return len(self.items) == 0
  ```
  - Time Complexity: O(1)
  - Returns `True` if the stack contains no elements, otherwise `False`
  - Essential for checking boundary conditions before operations

- **`push(item)`**: 
  ```python
  def push(self, item):
      self.items.append(item)
  ```
  - Time Complexity: O(1) amortized
  - Adds an element to the top of the stack
  - In Python, this uses the `append()` method of the underlying list

- **`pop()`**: 
  ```python
  def pop(self):
      return self.items.pop()
  ```
  - Time Complexity: O(1)
  - Removes and returns the topmost element
  - Raises `IndexError` if called on an empty stack

- **`peek()`**: 
  ```python
  def peek(self):
      return self.items[-1]
  ```
  - Time Complexity: O(1)
  - Returns the top element without removing it
  - Useful for inspecting the stack without modifying it

- **`size()`**: 
  ```python
  def size(self):
      return len(self.items)
  ```
  - Time Complexity: O(1)
  - Returns the number of elements in the stack

#### 1.1.2 Python Magic Methods:

The implementation includes Python's special methods (dunder methods) that allow the stack to behave like a native Python collection:

##### String Representation Methods:
- **`__str__(self)`**: Returns a string representation of the stack
- **`__repr__(self)`**: Returns a detailed string representation for debugging

##### Collection Behavior Methods:
- **`__len__(self)`**: Enables the `len()` function on the stack
- **`__contains__(self, item)`**: Supports the `in` operator (`item in stack`)
- **`__getitem__(self, index)`**: Enables indexing (`stack[index]`)
- **`__setitem__(self, index, value)`**: Enables assignment to indices (`stack[index] = value`)
- **`__delitem__(self, index)`**: Enables deletion of items by index (`del stack[index]`)
- **`__iter__(self)`**: Makes the stack iterable in a for loop
- **`_reversed__(self)`**: Supports the `reversed()` function

##### Comparison Operators:
- **`__eq__(self, other)`**: Equality comparison (`==`)
- **`__ne__(self, other)`**: Inequality comparison (`!=`)
- **`__gt__(self, other)`**: Greater than comparison (`>`)
- **`__ge__(self, other)`**: Greater than or equal comparison (`>=`)
- **`__lt__(self, other)`**: Less than comparison (`<`)
- **`__le__(self, other)`**: Less than or equal comparison (`<=`)

##### Arithmetic Operators:
- **`__add__(self, other)`**: Addition (`+`)
- **`__iadd__(self, other)`**: In-place addition (`+=`)
- **`__mul__(self, other)`**: Multiplication (`*`)
- **`__imul__(self, other)`**: In-place multiplication (`*=`)
- **`__truediv__(self, other)`**: Division (`/`)
- **`__itruediv__(self, other)`**: In-place division (`/=`)
- **`__floordiv__(self, other)`**: Integer division (`//`)
- **`__ifloordiv__(self, other)`**: In-place integer division (`//=`)
- **`__mod__(self, other)`**: Modulo (`%`)
- **`__imod__(self, other)`**: In-place modulo (`%=`)
- **`__pow__(self, other)`**: Exponentiation (`**`)
- **`__ipow__(self, other)`**: In-place exponentiation (`**=`)

##### Unary Operators:
- **`__neg__(self)`**: Negation (`-stack`)
- **`__pos__(self)`**: Positive (`+stack`)
- **`__abs__(self)`**: Absolute value (`abs(stack)`)

##### Mathematical Functions:
- **`__round__(self, n=None)`**: Rounding (`round(stack, n)`)
- **`__ceil__(self)`**: Ceiling (`math.ceil(stack)`)
- **`__floor__(self)`**: Floor (`math.floor(stack)`)

##### Hashing:
- **`__hash__(self)`**: Enables the stack to be used as a dictionary key

#### 1.1.3 Code Analysis:

The test code demonstrates various operations:

```python
if __name__ == "__main__":
    stack = Stack()
    stack.push(1)
    stack.push(2)
    stack.push(3)
    print(stack)  # Output: [1, 2, 3]
    print(stack.pop())  # Output: 3
    print(stack)  # Output: [1, 2]
    print(stack.peek())  # Output: 2
    print(stack.size())  # Output: 2
    print(stack.is_empty())  # Output: False
```

The test code also demonstrates various slicing operations that showcase the stack's list-like behavior:
- `stack.items[0]`: First element
- `stack.items[-1]`: Last element
- `stack.items[1:3]`: Slicing (elements at indices 1 and 2)
- `stack.items[:3]`: Slicing (all elements up to index 3)
- `stack.items[1:]`: Slicing (all elements from index 1 onwards)
- `stack.items[::2]`: Slicing with step (every other element)
- `stack.items[::-1]`: Reverse slicing (all elements in reverse order)
- Various other slicing operations with different step values

### 1.2 Copy 2 stacks without using extra memory

The code demonstrates copying one stack to another stack without using extra space maintaing the relative order with a demonstration of a stack reversal algorithm then copying the values:

```python
class Stack(object):
    def __init__(self):
        self.stack = []
```


#### 1.2.1 Stack Reversal Algorithm:

This code demonstrates a stack reversal algorithm:

```python
source = Stack()     
dest = Stack()         
source.push(1)
source.push(2)
source.push(3)

print("Source Stack:")
source.display()

count = 0

while count != source.length() - 1:
    
    topVal = source.pop()
    while count != source.length():
        dest.push(source.pop())
        
    source.push(topVal)
    while dest.length() != 0:
        source.push(dest.pop())
        
    count += 1

while source.length() != 0:
    dest.push(source.pop())
    
print("Destination Stack:")
dest.display()
```

This algorithm reverses a stack in-place using only stack operations (push and pop) and a temporary stack:

1. **Initial state**: 
   - Source stack: [1, 2, 3] (top is 3)
   - Destination stack: []

2. **Iteration 1** (count = 0):
   - Remove top element 3 from source
   - Move elements from source to dest until count (0) elements remain in source
     - Pop 2 from source, push to dest
     - Pop 1 from source, push to dest
   - Source now has [], dest has [1, 2]
   - Push 3 back to source: source = [3], dest = [1, 2]
   - Move all elements from dest back to source: source = [3, 2, 1], dest = []
   - count = 1

3. **Iteration 2** (count = 1):
   - Remove top element 1 from source
   - Move elements from source until count (1) elements remain in source
     - Pop 2 from source, push to dest
   - Source now has [3], dest has [2]
   - Push 1 back to source: source = [3, 1], dest = [2]
   - Move all elements from dest back to source: source = [3, 1, 2], dest = []
   - count = 2

4. **Iteration 3** (count = 2):
   - No operation (count = 2 equals source.length() - 1)

5. **Final Transfer**:
   - Move all elements from source to dest: source = [], dest = [2, 1, 3]

6. **Final state**:
   - Source stack: []
   - Destination stack: [2, 1, 3] (top is 3)

This algorithm demonstrates a stack reversal technique that strictly adheres to stack operations without using array indexing, maintaining the stack's LIFO property throughout the process.

### 1.3 Stack Applications

Stacks are used in various applications:

1. **Function Call Management**: Modern programming languages use a call stack to keep track of function calls.
   - Each function call pushes a new frame onto the stack
   - When a function returns, its frame is popped off the stack

2. **Expression Evaluation**: Stacks are used to evaluate expressions, especially in:
   - Infix to postfix conversion
   - Postfix expression evaluation
   - Arithmetic expression parsing

3. **Balanced Parentheses**: Checking if a string has balanced parentheses:
   - Push opening brackets onto the stack
   - Pop when a closing bracket is encountered and check if it matches

4. **Syntax Parsing**: Compilers and interpreters use stacks for parsing syntax.

5. **Undo Mechanism**: Applications use stacks to implement undo functionality.

6. **Browser History**: Web browsers use stacks to implement forward/backward navigation.

7. **Recursion Implementation**: Recursion can be implemented iteratively using a stack.

8. **Depth-First Search**: Graph traversal algorithms like DFS use stacks.

## 2. Tree Data Structures

A tree is a hierarchical data structure consisting of nodes connected by edges. Each node can have multiple children but only one parent (except for the root, which has no parent).

### 2.1 Basic Tree Implementation

The first `TreeNode` class implements a general tree where each node can have multiple children:

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []

    def add_child(self, child):
        self.children.append(child)

    def remove_child(self, child):
        self.children.remove(child)
```

#### 2.1.1 Core Tree Operations:

- **`add_child(child)`**: 
  - Adds a child node to the current node
  - Time Complexity: O(1)

- **`remove_child(child)`**: 
  - Removes a child node from the current node
  - Time Complexity: O(n) where n is the number of children (due to the list's removal operation)
  - Raises `ValueError` if the child is not found

#### 2.1.2 Test Code Analysis:

The test code builds a simple tree structure:

```python
if __name__ == "__main__":
    tree = TreeNode("A")
    tree.add_child(TreeNode("B"))
    tree.add_child(TreeNode("C"))
    tree.children[0].add_child(TreeNode("D"))
    tree.children[0].add_child(TreeNode("E"))
    tree.children[1].add_child(TreeNode("F"))
    tree.children[1].add_child(TreeNode("G"))
```

This creates the following tree structure:
```
    A
   / \
  B   C
 / \ / \
D  E F  G
```

The test then prints various references to nodes in the tree:
- `tree`: The root node A
- `tree.children`: The list of A's children [B, C]
- `tree.children[0]`: The first child B
- `tree.children[1]`: The second child C
- `tree.children[0].children`: The list of B's children [D, E]
- `tree.children[1].children`: The list of C's children [F, G]
- `tree.children[0].children[0]`: D
- `tree.children[0].children[1]`: E
- `tree.children[1].children[0]`: F
- `tree.children[1].children[1]`: G

### 2.2 Tree Traversal

Same as the basic implementation, plus:

- **`inorder_traversal()`**: 
  ```python
  def inorder_traversal(self):
      if self.children:
          for child in self.children:
              child.inorder_traversal()
      else:
          print(self.value)
  ```
  - Performs an inorder traversal of the tree
  - For each node, recursively traverses its children
  - If a node has no children (leaf node), prints its value
  - Time Complexity: O(n) where n is the number of nodes in the tree

#### 2.2.3 Test Code Analysis:

The test code for the enhanced TreeNode implementation creates a tree with the entire English alphabet:

```python
if __name__ == "__main__":
    tree = TreeNode("A")
    tree.add_child("B")
    tree.add_child("C")
    tree.add_child("D")
    # ... adds all letters of the alphabet as children of A
    tree.add_child("Z")
```

This creates a tree where all letters are direct children of the root node A:
```
        A
       /|\
      / | \
     B  C  ... Z
```

Unlike the previous tree implementation where each node was a TreeNode object, this test code adds string values directly as children, treating the TreeNode's children list as a container for arbitrary values rather than just TreeNode instances.

### 2.3 Tree Concepts and Terminology

#### 2.3.1 Core Tree Concepts:

- **Root**: The topmost node of a tree, which has no parent (node A in our examples)
- **Node**: Each element in a tree containing a value and references to other nodes
- **Edge**: The connection between two nodes
- **Parent**: A node that has one or more child nodes
- **Child**: A node that has a parent node
- **Leaf Node**: A node with no children (D, E, F, G in our first example)
- **Siblings**: Nodes that share the same parent (B and C are siblings)
- **Depth**: The distance (number of edges) from the root to a node
- **Height**: The maximum depth of any node in the tree
- **Subtree**: A tree consisting of a node and all its descendants
- **Binary Tree**: A tree where each node has at most two children
- **N-ary Tree**: A tree where each node can have at most N children

#### 2.3.2 Tree Traversal Algorithms:

1. **Depth-First Traversals**:
   - **Preorder** (Root → Left → Right):
     ```python
     def preorder(node):
         if node:
             print(node.value)  # Process the root
             for child in node.children:  # Process all children
                 preorder(child)
     ```
   - **Inorder** (Left → Root → Right): Only meaningful for binary trees but implemented in our second TreeNode class:
     ```python
     def inorder_traversal(self):
         if self.children:
             for child in self.children:
                 child.inorder_traversal()
         else:
             print(self.value)
     ```
   - **Postorder** (Left → Right → Root):
     ```python
     def postorder(node):
         if node:
             for child in node.children:
                 postorder(child)
             print(node.value)  # Process the root after children
     ```

2. **Breadth-First Traversal** (Level Order):
   ```python
   def level_order(root):
       if not root:
           return
       queue = [root]
       while queue:
           node = queue.pop(0)
           print(node.value)
           for child in node.children:
               queue.append(child)
   ```

### 2.4 Tree Applications

1. **File Systems**: Directories and files form a tree hierarchy
2. **Organization Charts**: Representing hierarchical relationships
3. **DOM in Web Browsers**: HTML documents are represented as trees
4. **Abstract Syntax Trees**: Used in compilers for parsing code
5. **Decision Trees**: Used in machine learning for classification
6. **Binary Search Trees**: Efficient data structures for lookups
7. **Heaps**: Special trees used in priority queue implementations
8. **Tries**: Specialized trees for string operations (discussed later)

## 3. Binary Search Tree (BST)

A Binary Search Tree is a specialized binary tree with the following properties:
- The left subtree of a node contains only nodes with values less than the node's value
- The right subtree contains only nodes with values greater than the node's value
- Both left and right subtrees are also BSTs

### 3.1 BST Implementation

```python
class BSTNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None
    
    def insert(self, value):
        if not self.root:
            self.root = BSTNode(value)
            return
        
        self._insert_recursive(self.root, value)
    
    def _insert_recursive(self, node, value):
        if value < node.value:
            if node.left is None:
                node.left = BSTNode(value)
            else:
                self._insert_recursive(node.left, value)
        else:
            if node.right is None:
                node.right = BSTNode(value)
            else:
                self._insert_recursive(node.right, value)
    
    def search(self, value):
        return self._search_recursive(self.root, value)
    
    def _search_recursive(self, node, value):
        if node is None or node.value == value:
            return node
        
        if value < node.value:
            return self._search_recursive(node.left, value)
        return self._search_recursive(node.right, value)
    
    def delete(self, value):
        self.root = self._delete_recursive(self.root, value)
    
    def _delete_recursive(self, root, value):
        if root is None:
            return root
        
        if value < root.value:
            root.left = self._delete_recursive(root.left, value)
        elif value > root.value:
            root.right = self._delete_recursive(root.right, value)
        else:
            # Node with only one child or no child
            if root.left is None:
                return root.right
            elif root.right is None:
                return root.left
            
            # Node with two children
            # Get inorder successor (smallest in right subtree)
            root.value = self._min_value_node(root.right).value
            root.right = self._delete_recursive(root.right, root.value)
        
        return root
    
    def _min_value_node(self, node):
        current = node
        while current.left is not None:
            current = current.left
        return current
    
    def inorder_traversal(self):
        result = []
        self._inorder_recursive(self.root, result)
        return result
    
    def _inorder_recursive(self, node, result):
        if node:
            self._inorder_recursive(node.left, result)
            result.append(node.value)
            self._inorder_recursive(node.right, result)
    
    def preorder_traversal(self):
        result = []
        self._preorder_recursive(self.root, result)
        return result
    
    def _preorder_recursive(self, node, result):
        if node:
            result.append(node.value)
            self._preorder_recursive(node.left, result)
            self._preorder_recursive(node.right, result)
    
    def postorder_traversal(self):
        result = []
        self._postorder_recursive(self.root, result)
        return result
    
    def _postorder_recursive(self, node, result):
        if node:
            self._postorder_recursive(node.left, result)
            self._postorder_recursive(node.right, result)
            result.append(node.value)
```

### 3.2 BST Operations

#### 3.2.1 Insertion

- **Time Complexity**: O(h) where h is the height of the tree
  - Best Case: O(log n) for a balanced tree
  - Worst Case: O(n) for a skewed tree
- **Space Complexity**: O(h) for recursion stack

The insertion algorithm:
1. If the tree is empty, create a new node as the root
2. Otherwise, compare the value with the current node:
   - If value < node.value, go to the left subtree
   - If value >= node.value, go to the right subtree
3. Repeat until finding an empty spot to insert the new node

#### 3.2.2 Search

- **Time Complexity**: O(h) where h is the height of the tree
  - Best Case: O(log n) for a balanced tree
  - Worst Case: O(n) for a skewed tree
- **Space Complexity**: O(h) for recursion stack

The search algorithm:
1. If the tree is empty or the current node contains the value, return the current node
2. If value < node.value, search in the left subtree
3. If value > node.value, search in the right subtree

#### 3.2.3 Deletion

- **Time Complexity**: O(h) where h is the height of the tree
- **Space Complexity**: O(h) for recursion stack

The deletion algorithm handles three cases:
1. **Node has no children**: Simply remove the node
2. **Node has one child**: Replace the node with its child
3. **Node has two children**: 
   - Find the inorder successor (smallest value in right subtree)
   - Replace the node's value with the successor's value
   - Delete the successor from the right subtree

#### 3.2.4 Traversal

1. **Inorder Traversal** (Left → Root → Right):
   - Visits nodes in ascending order
   - Used to get a sorted list of elements

2. **Preorder Traversal** (Root → Left → Right):
   - Used to create a copy of the tree
   - Used in prefix expression trees

3. **Postorder Traversal** (Left → Right → Root):
   - Used to delete a tree
   - Used in postfix expression trees

### 3.3 BST Applications

1. **Sorted Data Representation**: BSTs keep data in a sorted order
2. **Implementation of Symbol Tables**: Used in compilers
3. **Database Indexing**: Used for efficient lookup
4. **Priority Queues**: Used in scheduling and event-driven simulations
5. **Dictionary Implementation**: For fast lookups, insertions, and deletions

## 4. Trie Data Structure

A Trie (pronounced "try") is a specialized tree structure optimized for string operations. It is particularly efficient for storing and searching strings with common prefixes.

### 4.1 Trie Implementation from Code

```python
class TrieNode:
    def __init__(self):
        self.children = [None] * 26  # Array for lowercase English letters
        self.is_end_of_word = False


class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def get_index(self, char):
        return ord(char) - ord('a')
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char < 'a' or char > 'z':
                continue
            idx = self.get_index(char)
            if node.children[idx] is None:
                node.children[idx] = TrieNode()
            node = node.children[idx]
        node.is_end_of_word = True
    
    def search(self, word, arr):
        node = self.root
        for char in word:
            if char < 'a' or char > 'z':
                continue
            arr[0] += 1  # Increment comparison counter
            index = self.get_index(char)
            if node.children[index] is None:
                return False
            node = node.children[index]

        return node.is_end_of_word
```

### 4.2 Trie Concepts

#### 4.2.1 Structure:
- Each node contains an array (or map) of child nodes and a flag indicating if it's the end of a word
- The array size in this implementation is 26 (for lowercase English letters)
- Each index in the array corresponds to a letter (0 for 'a', 1 for 'b', etc.)
- If `node.children[i]` is not null, it means the character exists in the trie

#### 4.2.2 Core Operations:

1. **Insertion**:
   - Time Complexity: O(m) where m is the length of the word
   - Space Complexity: O(m) in worst case
   
   The algorithm:
   1. Start from the root
   2. For each character in the word:
      - Calculate the index (`ord(char) - ord('a')`)
      - If the child node doesn't exist, create a new node
      - Move to the child node
   3. Mark the last node as the end of a word

2. **Search**:
   - Time Complexity: O(m) where m is the length of the word
   - Space Complexity: O(1)
   
   The algorithm:
   1. Start from the root
   2. For each character in the word:
      - Calculate the index
      - Increment the comparison counter
      - If the child node doesn't exist, return false
      - Move to the child node
   3. Return true if the current node is marked as the end of a word

3. **Prefix Search** (not implemented in the code but a common trie operation):
   ```python
   def starts_with(self, prefix):
       node = self.root
       for char in prefix:
           if char < 'a' or char > 'z':
               continue
           index = self.get_index(char)
           if node.children[index] is None:
               return False
           node = node.children[index]
       return True
   ```
   - Returns true if any word in the trie starts with the given prefix

### 4.3 Trie Implementation Analysis

The provided Trie implementation focuses on lowercase English letters and includes:

1. **Character Mapping**:
   ```python
   def get_index(self, char):
       return ord(char) - ord('a')
   ```
   - Maps characters to array indices (a→0, b→1, ..., z→25)

2. **Non-Alphabet Character Handling**:
   ```python
   if char < 'a' or char > 'z':
       continue
   ```
   - Skips non-lowercase letters during insertion and search

3. **Performance Tracking**:
   ```python
   arr[0] += 1  # Increment comparison counter
   ```
   - Tracks the number of character comparisons during search

4. **File Integration**:
   ```python
   def read_words(filename):
       words = []
       with open(filename, 'r') as file:
           for line in file:
               word = line.strip()
               if word: 
                   words.append(word)
       return words
   ```
   - Reads words from a text file, one word per line

5. **Usage Demonstration**:
   ```python
   def main():
       trie = Trie()
       words = read_words("data.txt")
       
       for word in words:
           trie.insert(word)
       
       search_word = input("Word : ")
       time = [0]
       
       if trie.search(search_word, time):
           print(f"'{search_word}' was found in the trie in {time[0]} comparisons")
       else:
           print(f"'{search_word}' was not found in the trie")
   ```
   - Creates a trie from words in a file
   - Takes user input to search for a word
   - Reports success/failure and the number of comparisons

### 4.4 Trie Applications

1. **Autocomplete**: Suggests words as you type (Google search, text editors)
2. **Spell Checking**: Efficiently verifies if words exist in a dictionary
3. **IP Routing Tables**: Stores network prefixes for routing decisions
4. **Dictionary Implementation**: For fast prefix-based lookups
5. **Word Games**: Efficiently validates words (Scrabble, Boggle)
6. **Text Compression**: In certain compression algorithms like LZW
7. **Natural Language Processing**: For efficiently storing and retrieving vocabularies

### 4.5 Trie vs. Hash Table vs. BST

| Feature | Trie | Hash Table | BST |
|---------|------|------------|-----|
| Search Time | O(m) - m is word length | O(1) average, O(n) worst | O(log n) average, O(n) worst |
| Insert Time | O(m) | O(1) average, O(n) worst | O(log n) average, O(n) worst |
| Space Efficiency | High for common prefixes | Medium (depends on load factor) | Low |
| Prefix Search | O(m) | Not efficient | Not efficient |
| Sorted Traversal | Natural lexicographical order | Not sorted | In-order traversal is sorted |
| Worst Case | Rarely occurs | Hash collisions | Unbalanced tree |

## 5. LinkedList Implementation for Tree Traversal

While not explicitly shown in the provided code, LinkedList is commonly used to implement tree traversal algorithms. Here's how LinkedList can be used for various tree traversals:

### 5.1 LinkedList Node Definition

```python
class ListNode:
    def __init__(self, value=None):
        self.value = value
        self.next = None
```

### 5.2 LinkedList Implementation

```python
class LinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.size = 0
    
    def append(self, value):
        new_node = ListNode(value)
        if not self.head:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node
        self.size += 1
    
    def prepend(self, value):
        new_node = ListNode(value)
        if not self.head:
            self.head = new_node
            self.tail = new_node
        else:
            new_node.next = self.head
            self.head = new_node
        self.size += 1
    
    def remove_first(self):
        if not self.head:
            return None
        
        value = self.head.value
        self.head = self.head.next
        if not self.head:
            self.tail = None
        self.size -= 1
        return value
    
    def is_empty(self):
        return self.size == 0
    
    def __len__(self):
        return self.size
```

### 5.3 Tree Traversals Using LinkedList

#### 5.3.1 Breadth-First Traversal (Level Order) Using LinkedList as Queue

```python
def level_order_traversal(root):
    if not root:
        return []
    
    result = []
    queue = LinkedList()
    queue.append(root)
    
    while not queue.is_empty():
        node = queue.remove_first()
        result.append(node.value)
        
        # Add all children to the queue
        for child in node.children:
            queue.append(child)
    
    return result
```

#### 5.3.2 Depth-First Traversal Using LinkedList as Stack

```python
def dfs_traversal(root):
    if not root:
        return []
    
    result = []
    stack = LinkedList()
    stack.prepend(root)  # Use prepend for stack behavior
    
    while not stack.is_empty():
        node = stack.remove_first()
        result.append(node.value)
        
        # Add all children to the stack (in reverse for proper DFS order)
        for child in reversed(node.children):
            stack.prepend(child)
    
    return result
```

### 5.4 Path Finding in Trees Using LinkedList

```python
def find_path(root, target_value):
    if not root:
        return None
    
    path = LinkedList()
    
    if _find_path_recursive(root, target_value, path):
        return path
    else:
        return None

def _find_path_recursive(node, target_value, path):
    # Add current node to the path
    path.append(node.value)
    
    # If current node is the target, return true
    if node.value == target_value:
        return True
    
    # Check all children
    for child in node.children:
        if _find_path_recursive(child, target_value, path):
            return True
    
    # If target not found in subtree, remove current node from path
    path.remove_first()  # Assumes we track the node to remove
    return False
```

## 6. Binary Search Tree (BST) Advanced Operations

### 6.1 Balancing a BST

A balanced BST has a height of O(log n), ensuring optimal time complexity for operations. Here's how to balance a BST:

```python
def balance_bst(root):
    # Step 1: Store nodes in sorted order via inorder traversal
    nodes = []
    _inorder_to_array(root, nodes)
    
    # Step 2: Recursively build a balanced tree
    return _build_balanced_bst(nodes, 0, len(nodes) - 1)

def _inorder_to_array(node, nodes):
    if node:
        _inorder_to_array(node.left, nodes)
        nodes.append(node.value)
        _inorder_to_array(node.right, nodes)

def _build_balanced_bst(nodes, start, end):
    if start > end:
        return None
    
    # Get middle element as the root
    mid = (start + end) // 2
    root = BSTNode(nodes[mid])
    
    # Recursively build left and right subtrees
    root.left = _build_balanced_bst(nodes, start, mid - 1)
    root.right = _build_balanced_bst(nodes, mid + 1, end)
    
    return root
```

### 6.2 Self-Balancing BSTs

Several types of self-balancing BSTs maintain balance automatically:

1. **AVL Tree**:
   - Maintains a balance factor (height difference between left and right subtrees) ≤ 1
   - Performs rotations after insertions/deletions to maintain balance
   - Operations have O(log n) time complexity

2. **Red-Black Tree**:
   - Each node is colored red or black
   - Has specific rules about node colors and path lengths
   - Less strictly balanced than AVL trees but still O(log n) operations
   - Used in many language standard libraries (C++ STL, Java TreeMap/TreeSet)

3. **B-Tree**:
   - Generalizes BST to allow more than two children per node
   - Often used in databases and file systems
   - Well-suited for systems that read/write large blocks of data

### 6.3 Range Queries in BST

Finding all values in a given range [min, max]:

```python
def range_query(root, min_val, max_val):
    result = []
    _range_query_recursive(root, min_val, max_val, result)
    return result

def _range_query_recursive(node, min_val, max_val, result):
    if not node:
        return
    
    # If node.value > min_val, search left subtree
    if min_val < node.value:
        _range_query_recursive(node.left, min_val, max_val, result)
    
    # Add current node if it's in range
    if min_val <= node.value <= max_val:
        result.append(node.value)
    
    # If node.value < max_val, search right subtree
    if max_val > node.value:
        _range_query_recursive(node.right, min_val, max_val, result)
```

## 7. Advanced Trie Operations

### 7.1 Auto-Complete Implementation

```python
def autocomplete(trie, prefix, max_suggestions=10):
    # Find the node corresponding to the prefix
    node = trie.root
    for char in prefix:
        if char < 'a' or char > 'z':
            continue
        index = trie.get_index(char)
        if node.children[index] is None:
            return []  # Prefix not found
        node = node.children[index]
    
    # Find all words with the given prefix
    suggestions = []
    _find_all_words(node, prefix, suggestions, max_suggestions)
    return suggestions

def _find_all_words(node, prefix, suggestions, max_suggestions):
    if len(suggestions) >= max_suggestions:
        return
    
    if node.is_end_of_word:
        suggestions.append(prefix)
    
    for i in range(26):
        if node.children[i]:
            char = chr(ord('a') + i)
            _find_all_words(node.children[i], prefix + char, suggestions, max_suggestions)
```

### 7.2 Wildcard Pattern Matching

Supporting wildcard searches like "c*t" (matches "cat", "cot", etc.):

```python
def wildcard_search(trie, pattern):
    return _wildcard_search_recursive(trie.root, pattern, 0)

def _wildcard_search_recursive(node, pattern, index):
    if index == len(pattern):
        return node.is_end_of_word
    
    char = pattern[index]
    
    if char == '*':  # Wildcard character
        # Try all possible characters at this position
        for i in range(26):
            if node.children[i] and _wildcard_search_recursive(node.children[i], pattern, index + 1):
                return True
        return False
    else:
        # Regular character match
        char_index = ord(char) - ord('a')
        if node.children[char_index] is None:
            return False
        return _wildcard_search_recursive(node.children[char_index], pattern, index + 1)
```

### 7.3 Compressed Trie (Radix Tree)

A space-optimized version of a trie that merges nodes with single children:

```python
class RadixNode:
    def __init__(self):
        self.children = {}  # Dictionary instead of array
        self.is_end_of_word = False

class RadixTree:
    def __init__(self):
        self.root = RadixNode()
    
    def insert(self, word):
        if not word:
            return
        
        self._insert_recursive(self.root, word)
    
    def _insert_recursive(self, node, suffix):
        # If we're at the end of the suffix, mark this node as end of word
        if not suffix:
            node.is_end_of_word = True
            return
        
        # Check if there's a matching prefix in any of the children
        for prefix, child in node.children.items():
            # Find the common prefix between suffix and this child's prefix
            common_length = 0
            while common_length < min(len(prefix), len(suffix)) and prefix[common_length] == suffix[common_length]:
                common_length += 1
            
            if common_length > 0:
                # There is some overlap
                if common_length == len(prefix):
                    # Complete match with this child's prefix
                    # Continue insertion with remaining suffix
                    self._insert_recursive(child, suffix[common_length:])
                else:
                    # Partial match, split the existing prefix
                    # Create a new intermediate node
                    new_node = RadixNode()
                    
                    # Update the current node's children
                    node.children[prefix[:common_length]] = new_node
                    new_node.children[prefix[common_length:]] = child
                    
                    # Delete the old prefix
                    del node.children[prefix]
                    
                    # Insert the remaining suffix
                    if common_length < len(suffix):
                        self._insert_recursive(new_node, suffix[common_length:])
                    else:
                        new_node.is_end_of_word = True
                
                return
        
        # No matching prefix found, add a new child
        new_node = RadixNode()
        new_node.is_end_of_word = True
        node.children[suffix] = new_node
```

## 8. Memory Efficiency and Time Complexity Analysis

### 8.1 Memory Complexity

| Data Structure | Memory Complexity | Notes |
|----------------|-------------------|-------|
| Stack (Array-based) | O(n) | Fixed capacity or dynamic resizing |
| Stack (LinkedList-based) | O(n) | Additional space for pointers |
| Binary Tree | O(n) | Each node has value and two pointers |
| General Tree | O(n) | Each node has value and array/list of children |
| BST | O(n) | Balanced or unbalanced |
| Trie | O(n×m) | n words of average length m |
| Compressed Trie | O(n) | Better than standard trie for sparse datasets |

### 8.2 Time Complexity Comparison

| Operation | Stack | BST (Balanced) | BST (Unbalanced) | Trie |
|-----------|-------|----------------|------------------|------|
| Insert | O(1) | O(log n) | O(n) | O(m) |
| Delete | O(1) | O(log n) | O(n) | O(m) |
| Search | O(n) | O(log n) | O(n) | O(m) |
| Min/Max | O(n) | O(log n) | O(n) | N/A |
| Successor/Predecessor | O(n) | O(log n) | O(n) | N/A |
| Prefix Search | N/A | O(n) | O(n) | O(m) |

Where:
- n: Number of elements/nodes
- m: Length of the word/key
- h: Height of the tree

### 8.3 Practical Considerations

1. **Locality of Reference**:
   - Array-based implementations (like our first Stack) often have better cache performance
   - Node-based structures may suffer from cache misses due to pointer chasing

2. **Memory Overhead**:
   - Pointers in tree nodes add significant overhead
   - Tries can be memory-intensive for large alphabets

3. **Implementation Complexity**:
   - Balancing BSTs adds significant implementation complexity
   - Tries are relatively simple to implement but may require optimizations

4. **Use Case Dependencies**:
   - For string operations, tries generally outperform BSTs
   - For general ordered data, balanced BSTs are often preferred
   - For LIFO operations, stacks are unbeatable

## 9. Real-World Applications and Use Cases

### 9.1 Stack Applications

1. **Function Call Management**: Modern programming languages use a call stack
2. **Expression Evaluation**: Calculators and expression parsers
3. **Syntax Parsing**: Compilers and interpreters
4. **Backtracking Algorithms**: Maze solving, puzzle solutions
5. **Browser History**: Back and forward navigation
6. **Undo Mechanisms**: Text editors and graphic design software

### 9.2 Tree Applications

1. **File Systems**: Directory hierarchies
2. **Organization Charts**: Company structures
3. **XML/HTML DOM**: Web browsers and parsers
4. **Decision Trees**: AI and machine learning classifiers
5. **Game Trees**: AI for games like chess and Go
6. **Syntax Trees**: Compilers and interpreters

### 9.3 BST Applications

1. **Database Indexing**: Efficient lookup structures
2. **Priority Queues**: Job scheduling
3. **Sorted Data Management**: Maintaining ordered collections
4. **Symbol Tables**: Compiler implementations
5. **Range Queries**: Finding all data within bounds

### 9.4 Trie Applications

1. **Autocomplete Systems**: Search engines, text editors
2. **Spell Checkers**: Word processors
3. **IP Routing**: Network routers using CIDR notation
4. **T9 Predictive Text**: Mobile phone keyboards
5. **Genome Analysis**: DNA sequence matching

## 10. Advanced Implementation Techniques

### 10.1 Thread-Safe Implementations

```python
import threading

class ThreadSafe