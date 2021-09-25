# Class 02

## Two pointer method
When you use 2 pointers on an array to traverse the array. The pointers can run either end until start pointer gets larger than end pointer (the middle of the array)

```python 
# Time complexity: O(n)  --> We traversed the whole length of the array.
# Space complexity: O(n) --> Because we used another array equal to the size of the string `a`.

a = 'racecar`
b = ''
for char in a:
    b = b + char
for i in range(len(a)):
    if a[i] != b[i]:
        return False        # Not a palindrome
return True                 # Yes. It's a palindrome.
```

    
```python
# Time complexity: O(n)  --> We traversed the half of length of the array.
# Space complexity: O(1) --> Because we didn't create any additional array.

a = 'racecar'
start = 0
end = len(a)-1
while start <= end:
    if a[start] != a[end]:
        return False        # Not a palindrome.
    start += 1
    end -= 1
return True                 # Yes. It's a palindrome.
```

In the above code, we checked if a string and its reverse string is same. If it's same, then this type of string is called palindrome.


## Python
### Python Class
To represent the real-world object into python, we use the class notation. 

Class has 
- attributes / properties / characteristics --> represented as nouns.
- behaviours / methods / functions / <what-it-can-do> / actions --> represented as verbs. 

```python
class Human:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def getAge(self):
        return self.age
        
    def walk(self):
        print('Walking...')
        
h1 = Human('James', 10)
h1.walk()
```
The `__init__` is called the constructor function.

### Mutable and Immutable 
Mutable Ojbects
- Lists
- Sets
- Dictionaries
- User-defined classes

Immutable Objects
- Numbers
- Strings
- Tuples
- Frozen Sets
- User-defined classes




## PCB
When a program runs, then kernel sets some area for the process (running program).
- Heap area
- Stack area
- local variable area
- global variable area
- data (machine code of the program)
As a whole, it's called PCB (Program Control Block)

Objects are created in the heap area.
Objects references will be saved in stack area.

```python
h1 = Human()
```
`Human` object will be heap area. 
The variable `h1` will be created in stack area and hold the reference to the `Human` object. 
    
    



# LeetCode
## Problem 35


```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        start = 0
        end = len(nums) - 1

        while start <= end:
            mid = (start + end ) // 2
            if target == nums[mid]:
                return mid
            elif target < nums[mid]:
                end = mid - 1
            elif target > nums[mid]:
                start = mid + 1
        return start
```

**Case 1**
```python
nums = [1, 3, 5, 6]
target = 7
```
| start | end | mid         | nums[mid] | comparison |
|-------|-----|-------------|-----------|------------|
| 0     | 3   | (0+3)//2=1  | 3         | 3 < 7      |
| 2     | 3   | (2+3)//2=2  | 5         | 5 < 7      |
| 3     | 3   | (3+3)//2=3  | 6         | 6 < 7      |
| 4     | 3   | loop breaks |           |            |

`return start` => `return 4`

**Case 2**
```python
nums = [1, 3, 5, 6]
target = 6
```
| start | end | mid         | nums[mid] | comparison |
|-------|-----|-------------|-----------|------------|
| 0     | 3   | (0+3)//2=1  | 3         | 3 < 6      |
| 2     | 3   | (2+3)//2=2  | 5         | 5 < 6      |
| 3     | 3   | (3+3)//2=3  | 6         | 6 == 6     |

`return mid` => `return 3`

**Case 2**
```python
nums = [1, 3, 5, 6]
target = -1
```
| start | end | mid         | nums[mid] | comparison |
|-------|-----|-------------|-----------|------------|
| 0     | 3   | (0+3)//2=1  | 3         | -1 < 3     |
| 0     | 0   | (2+3)//2=0  | 1         | -1 < 1     |
| 0     | -1  | loop breaks |           |            |

`return start` => `return 0`
