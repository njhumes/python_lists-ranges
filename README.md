# Python Containers and Ranges

---
## Learning Objectives
<br>

<p>Students will be able to:</p>

- Use _lists_, _tuples_  as containers for data

- Use _list comprehensions_ to create lists

- Use a _range_ and a _for_ statement to loop through a range of integers

- Create subsets of a _sequence_ using the _slice_ operator


### General Purpose Containers
<br>

- As you know by now, applications frequently need to maintain collections of data within a _container_ data type.

- **What did we use in JS to hold collections of data?**

- In this lesson, we're going to review the following Python built-in types commonly used as _containers_:
	- **lists**
	- **tuples**

## Lists

---
### Lists - Purpose
<br>

- **Lists** are to Python as **arrays** are to JS.

- A **list** provides a container for zero or more items (_elements_).

- **Lists** can contain items of different types, including _dictionaries_ and nested _lists_.

- **List** have a class (type) of `list`.

---
### Lists - Basic Syntax
<br>

- Like _arrays_ in JS, a **list** is created with a set of _square brackets_:

	```python
	colors = ['red', 'green', 'blue'] 
	```

- The number of items in a _list_ is returned using the built-in `len()` function:

	```python
	len(colors)
	> 3
	```
---
### Lists - Features
<br>

<p><em>Lists</em> have the following features:

- They are considered to be a _sequence_ type in Python. A _sequence_ is a generic term used for an **ordered** collection. Other _sequence_ types in Python include _strings_ and _tuples_.

- They are mutable:

 	- Items within the _list_ can be replaced
 	- Items can be added and removed from a _list_

---
### Lists - Accessing Elements

- Accessing the individual elements of a _list_ is much like that as accessing elements in a JS array, i.e., by using an expression that evaluates to an _integer_ within _square brackets_:

	```python
	idx = 1
	colors[idx + 1]
	> blue
	```

- However, unlike in JS, we can use negative integers to index from the end of a _list_:

	```python
	colors[-1]
	> blue
	```
	No need to write code like `colors[len(colors) - 1]` - yay!


---
### Lists - Assigning Elements
<br>

- We also use square brackets to target an element of a _list_ for assignment:

	```python
	colors[-1] = 'brown'
	print(colors)
	> ['red', 'green', 'brown']
	```

---
### Lists - Adding Elements
<br>

- The equivalent to JS's `push()` method is `append()`:

	```python
	colors.append('purple')
	```
	
	However, unlike JS's `push()` method, `append()` can only add one item and does not return a value.
	
- For adding multiple items, use the `extend()`:

	```python
	colors.extend(['orange', 'black'])
	```

---
### Lists - Inserting Elements
<br>

- To add items to anywhere but the end of a _list_, use the `insert()` method:

	```python
	print(colors)
	> ['red', 'green', 'brown', 'purple', 'orange', 'black']
	colors.insert(1, 'yellow')
	> ['red', 'yellow', 'green', 'brown', 'purple', 'orange', 'black']
	```

---
### Lists - Deleting Elements
<br>

- Yup, there's a `pop()` method, but it's more flexible in Python because you can specify the index of the element to remove and return:

	```python
	print(colors)
	> ['red', 'yellow', 'green', 'brown', 'purple', 'orange', 'black']
	green = colors.pop(2)
	print(colors)
	> ['red', 'yellow', 'brown', 'purple', 'orange', 'black']
	```

---
### Lists - Deleting Elements
<br>

- If you don't care about the value returned by `pop()`, you can also use the `del` operator to delete items:

	```python
	print(colors)
	> ['red', 'yellow', 'brown', 'purple', 'orange', 'black']
	del colors[1]
	print(colors)
	> ['red', 'brown', 'purple', 'orange', 'black']
	```

---
### Lists - Deleting Elements
<br>

- Also there's a `remove()` method that removes the first item that matches what you pass in:

	```python
	print(colors)
	> ['red', 'brown', 'purple', 'orange', 'black']
	colors.remove('orange')
	print(colors)
	> ['red', 'brown', 'purple', 'black']
	```
	No value is returned by the `remove()` method.

---
### Lists - Clearing
<br>

- Lastly, `clear()` does just what you think:

	```python
	print(colors)
	> ['red', 'brown', 'purple', 'black']
	colors.clear()
	print(colors)
	> []
	```

---
### Lists - Iteration
<br>

- The `for` loop is used to iterate over the items in a _list_:

	```python
	colors = ['red', 'green', 'blue']
	for color in colors:
		print(color)
	> red
	> green
	> blue
	```

---
### Lists - Iteration
<br>

- If we need to access the index of the item while iterating a _list_, we use the built-in `enumerate()` function to provide the index and the value to a `for` loop:

	```python
	for idx, color in enumerate(colors):
		print(idx, color)
	> 0 red
	> 1 green
	> 2 blue
	```

---
## Dictionary & List Review

- **What are _dictionaries_ similar to in JS?**

- **What are _lists_ similar to in JS?**

- **Why won't the follow code work?**

	```python
	menu = {
		hamburger: 4.99,
		french_fries: 1.99,
		taco: 2.99
	}
	```

- **What is a way to add items to a _list_?**

- **What is a way to remove an item from the front of a _list_?**

---
## List Comprehensions

---
### List Comprehensions
<br>

- One of the most powerful features in Python are _list comprehensions_.

- _List comprehensions_ provide a concise way to create and work with lists.

- They will probably seem a little confusing as first, but they certainly are a favorite of _Pythonistas_ and you will certainly come across them when googling.

- Also, _comprehensions_ can be used similarly to create _dictionaries_ too.

---
### List Comprehensions<br><small>Numerical Example</small>
<br>

- If we needed to square all of the numbers in a _list_ and put them into a new _list_, we might use a for loop like this:

	```python
	nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
	
	# I want 'n * n' for each 'n' in nums 
	squares = []
	for n in nums:
		squares.append(n * n)
	print(squares)
	> [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
	```

- **What method in JS would we use in this scenario?**

---
### List Comprehensions<br><small>Numerical Example</small>

- A _list comprehension_ can reduce this code:

	```python
	# I want 'n * n' for each 'n' in nums 
	squares = []
	for n in nums:
		squares.append(n * n)
	```
	To this:
	
	```python
	# I want 'n * n' for each 'n' in nums 
	squares = [n * n for n in nums]
	```

- The _comprehension_ is basically an advanced `for` loop within _square brackets_ which, of course, returns a new _list_.

---
### List Comprehensions - Basic Syntax
<br>

- Here's the basic syntax of a _list comprehension_:

	```python
	# [<expression> for <item> in <list>]
	# This reads as: I want <expression> for each <item> in <list>
	```

---
### List Comprehensions - Filtering

- We've seen how _list comprehensions_ are a nice way to map a list, but they can be used for **filtering** too.

- Just like before, let's first look at how we would use a `for` loop to map and filter simultaneously:

	```python
	nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
	
	# I want 'n * n' for each 'n' in nums  if 'n * n' is even
	even_squares = []
	for n in nums:
		square = n * n 
		if square % 2 == 0:
			even_squares.append(square)
	print(even_squares)
	> [4, 16, 36, 64, 100]
	```


---
### List Comprehensions - Filtering

- Again _list comprehensions_ reduce the mapping and filtering from:

	```python
	# I want 'n * n' for each 'n' in nums  if 'n * n' is even
	even_squares = []
	for n in nums:
		square = n * n 
		if square % 2 == 0:
			even_squares.append(square)
	```
	To this one-liner:
	
	```python
	# I want 'n * n' for each 'n' in nums  if 'n * n' is even
	even_squares = [n * n for n in nums if (n * n) % 2 == 0]
	```
	Nice and readable!

---
### List Comprehensions - Review
<br>

- **What characters start and end a _list comprehension_**

- **Do _list comprehensions_ create or loop through lists?**

---
### List Comprehensions - Summary
<br>

- We've only scratched the surface of _list comprehensions_.

- They can even be used to create lists of _tuples_ that would otherwise require nested `for` loops.

- Speaking of **tuples**...

---
## Tuples

---
### Tuples - Purpose
<br>

- **Tuples** in Python are very similar to **lists**.

- _Tuples_ have a class (type) of `tuple`.

---
### Tuples - Basic Syntax
<br>

- _Tuples_ can be defined in a few different ways.  Most basically, they are defined like this:

	```python
	colors = ('red', 'green', 'blue')
	print(colors)
	> ('red', 'green', 'blue')
	print( len(colors) )
	> 3
	``` 
	Although it seems that _parentheses_ are used to create _tuples_, it's actually the _commas_.

---
### Tuples - Basic Syntax
<br>

- _Tuples_ can be created without using any parentheses:

	```python
	colors = 'red', 'green', 'blue'
	print(type(colors))
	> <class 'tuple'>
	```

- However, creating single-item _tuples_ without parens requires a trailing comma:

	```python
	colors = 'purple',  # tuple, not a string
	print(type(colors), len(colors))
	> <class 'tuple'> 1
	print(colors)
	> ('purple',)
	```

---
### Differences Between Tuples & Lists

- _Tuples_ are immutable, so they are great for protecting data that you don't want changed.

- Because they are immutable, iterating over _tuples_ is faster than with _lists_. They can also be used as _keys_ for _dictionaries_.

- Generally, you'll find that _tuples_ are used to contain heterogeneous (different) data types and _lists_ for homogeneous (similar) data types.

- _Tuples_ are often classified based on how many elements they contain, e.g., a **2-tuple** would be used to hold a `key` and its `value`.

---
### Tuples - Accessing Elements

- Although _tuples_ can't be modified like _lists_, we can retrieve their elements in exactly the same way:

	```python
	colors = ('red', 'green', 'blue')
	green = colors[1]
	print(green)
	> green
	```
- _Sequences_ also have an `index()` method that returns the index of the first match:

	```python
	colors = ('red', 'green', 'blue')
	blue_idx = colors.index('blue')
	print(blue_idx)
	> 2
	```
	
---
### Tuples - Iteration
<br>

- Just like with _lists_, other _sequences_ are iterated upon in the same way - by using `for` loops:

	```python
	colors = ('red', 'green', 'blue')
	for idx, color in enumerate(colors):
		print(idx, color)
	> 0 red
	> 1 green
	> 2 blue
	```

---
### Tuples - Unpacking
<br>

- _Tuples_ have a convenient feature, called _unpacking_, for doing multiple variable assignment:

	```python
	colors = ('red', 'green', 'blue')
	red, green, blue = colors
	print(red, green, blue)
	> red green blue
	```
	A tuple of variables on the left-side of the assignment operator and a tuple of values on the right is all it takes.

---
### Ranges - Purpose
<br>

- Although not a general purpose container, **ranges** are a _sequence type_ like _lists_ and _tuples_.

- The **range** type represents an immutable sequence of numbers and is commonly used for looping a specific number of times in `for` loops.

- _Ranges_ have a class (type) of `range`.

---
### Ranges - Basic Syntax
<br>

- **Ranges** can only be created by invoking the `range()` class:

	```python
	for num in range(5):
		print(num)
	> 0
	> 1
	> 2
	> 3
	> 4
	```
	Notice that by default, the sequence starts at `0` and goes up to, but does not including the integer passed in.

---
### Ranges - Basic Syntax
<br>

- _Ranges_ can also generate sequences with a **start** and a **step**:

	```python
	for even in range(2, 10, 2):
		print(even)
	> 2
	> 4
	> 6
	> 8
	```

- When not passed in, the _start_ value defaults to `0` and the _step_ defaults to `1`.

---
### Ranges - Basic Syntax
<br>

- _Ranges_ can also be used to create _lists_ and _tuples_:

	```python
	nums = list(range(10))
	print(nums)
	> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
	odds = tuple(range(1, 10, 2))
	print(odds)
	> (1, 3, 5, 7, 9)
	```

---
### Ranges - Negative Step
<br>

- If the _step_ is a negative integer, the _sequence_ counts down:

	```python
	for num in range(5, 0, -1):
		print(num)
	> 5
	> 4
	> 3
	> 2
	> 1
	```

---
## Sequences Can Be "Sliced"

---
### Slicing Sequences
<br>

- Python is known for having some cool tricks up its sleeve, for one, there's the "slice" operator (`[m:n]`).

- Since _sequence_ types are a collection of items (BTW, characters are the items in a _string_), we should be to target any subset of those items. We can, and those subsets are called _slices_.

---
### Slicing Sequences
<br>

- Just like with indexing, slicing uses _square brackets_, but adds a _colon_:

	```python
	short_name = 'Alexandria'[0:4]
	print(short_name)
	> Alex
	```

- Note that the slice includes up to, but not including the index to the right of the colon.

---
### Slicing Sequences
<br>

- If the first index is omitted, the slice copies the _sequence_ starting at the beginning:

	```python
	colors = ('red', 'green', 'blue')
	print( colors[:2] )
	> ('red', 'green')
	```
 
- If the up to index is omitted, the slice copies the _sequence_ all the way to the end:

	```python
	colors = ['red', 'green', 'blue']
	print( colors[1:] )
	> ['green', 'blue']
	```

---
### Slicing Sequences - Question
<br>

- **What would the value of `fruit_copy` be?**

	```python
	fruit = ('apples', 'bananas', 'oranges')
	fruit_copy = fruit[:]
	```

---
## Conclusion
<br>

- Python offers amazing power, convenience and readability with features such as _list comprehensions_ and _slicing_.

- However, as usual, it takes practice to become "comfortable" with these concepts, so on to the lab...
