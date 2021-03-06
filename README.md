# python-refresh
Quick crash course over basic Python 3 language features in preparation for
ClickToStart's Programming course. You should take some time and go over the 
official Python tutorial https://docs.python.org/3/tutorial/, this is just to
quickly go through core features you should be familiar with. These notes were
greatly inspired by [University of Edinburgh Informatics lab
notes](http://www.inf.ed.ac.uk/teaching/courses/inf2a/tutorials/2016_inf2a_P01_exercises.pdf).

The code we are writing here would work on all of Python 3 versions (and the 
vast majority on Python 2 as well) But you should use version 3.6 as it's the 
latest and greatest at the time of writing.

# Interpreted or Compiled?
Python is a programming language, a formal language specification designed to 
give instructions to a computer. The Python language has many implementations: 
* CPython: the reference implementation for Python, and the one you probably
installed from the main website. CPython is an interpreter, but it first
compiles the Python source code to an intermediary byte code. The byte code is
what's interpreted.
* PyPy: a Python interpreter built with Python itself (a subset of Python to be
technical). It does [Just-in-Time
Compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation) and is 
known to be quicker than CPython in many cases.
* Jython: Python which runs on the JVM
* IronPython: Python which runs on .NET framework and Mono

# Mind Your Space
Whitespace is important in Python. If you come from a language background with
brackets and the like, welcome to The Light! Indentation determines scope. For
indentation we'll be use 4 spaces as guided by
[PEP-8](https://www.python.org/dev/peps/pep-0008/).

# Numbers
The usual operators you've seen in Java/C/etc are all here as well:
+, -, *, /, %. Run Python on your shell `python3` and type the following:

```python    
5 + 3 # = 8
2 * 8 # = 16
3 / 2 # = 1.5
10 - 9 # = 1
13 % 3 # = 1

# You also figured that comments begin with # and go till the end of the line
# Note the division in of 3/2 returns 1.5. If you used Python 2 that division
# would return 1 as the numbers weren't explicitly floats. No need to worry 
# about that in version 3 :)

# To get that division that also floors the result do like the following
3 // 2 # = 1

# In Python, exponents use **
2**5 # = 32
```

# Strings
Strings can be represented with either single or double quotes


```python
'hi there'
"doing ok"
'what a horrible, invalid string!" # This wouldn't work
# The important thing is to be consistent. Pick one and keep up with it!

# You can concatenate strings with the plus sign
'hello ' + 'world' # hello world

# You can also repeat a string with the multiply sign
'Nana ' * 4 + 'Batman!'

# You can also access elements of a string by their index (starts from 0)
big_whale = 'Moby Dick'
big_whale[0] # 'M'
big_whale[5] # 'D'

# You can use negative indices to access elements from the right of the string
big_whale[-1] # 'k'
big_whale[-3] # 'i'

# Strings are immutable
sing_along = 'can\'t touch this' # Escape ' to use them in single quotes
sing_along[2] = 'u' # TypeError: 'str' object does not support item assignment
```

Some strings are really long. Actually, it's common Python convention to put a 
long string immediately after the first line of a module, function, class or
method definition. Long strings are used as docstring

```python
'''
Roses are red
Violets are blue
Doubles with mango is sweet
But not as good as you
'''
# Do not recite the above lines to someone else please...
"""
Docstrings normally use double quotes.
We'll maintain that convention for this course
"""
```

# Booleans
Python has two boolean values: True and False. Booleans inherit from integers,
so you can add and multiply them like numbers. True is 1 and False is 0

```python
True + True # = 2
True * 7 # = 7
False - 5 # 0
```

## Conditions
Well Booleans aren't fun for additions and other mathematical operators. We use
them to test for truthfullness. Or truthiness. Truth. We can write expressions
which evaluate to True or False:

```python
True and True # = True, using and is much easier than && right?
True or False # = True, more English words please
not True # = False
```

We can do comparisons on other Data Types as well

```python
8 == 2 * 4 # = True, == test equality, strings can be tested as well
'hi' == "  hi\t".strip() # strip function removes whitespace characters

2**7 != 64 # = True, test inequality

# Greater than or less than
4 > 2
19 < 19.5

# Greater/less than or equal to
23 >= 23
-42 <= -37

# Python also has "is". People use it interchangeably with == but that's not
# entirely correct. The is keyword checks if the two things being compared 
# points to the same object. == checks if two values being referenced have the
# same value
1000 is 10**3 # False
1000  == 10**3 # True
# Python caches small numerical and string objects, so is can work for some
# values. Be wary as many a bad bugs can arise as a result
```
In addition to the docs, you can read this about is:
https://stackoverflow.com/questions/132988/is-there-a-difference-between-and-is-in-python

# Lists
Lists are awesome containers for storing a variety of objects

```python
things_guaranteed_in_life = ['death', 'taxes', 'a new fifa game every year']

# You can add an item to a list by the append method
things_guaranteed_in_life.append('another transformers movie')

# You can extend the list with another list via plus
things_guaranteed_in_life + ['call of duty']
# Note that the above doesn't change the list contents, if you want it saved
# then you'll have to assign a variable to that value
things_guaranteed_in_life = things_guaranteed_in_life + ['call of duty']
# Or for brevity's sake
things_guaranteed_in_life += ['call of duty']

# Lists can have multiple data types stored in it
random_list_of_things = [88.9, 'the meaning of life', 42, False]

# Lists can be nested
matrix = [[0,0,0], [1,1,1], [-543, -989, -471]]
```

You can access individual elements of a list like you did with strings
```python
things_guaranteed_in_life[0] # 'death'
things_guaranteed_in_life[3] # 'another transformers movie'
things_guaranteed_in_life[-1] # 'call of duty'
things_guaranteed_in_life[-3] # 'a new fifa game every year'
```

Unlike strings, list are mutable
```python
random_list_of_things[1] = 'inside out'
random_list_of_things # [88.9, 'inside out', 42, False]
```

## More List Methods
```python
l1 = ['a', 'b', 'c', 'e']
# While append adds to end of the list, you can insert to a particular index
l1.insert(3, 'd') # l1 = ['a', 'b', 'c', 'd', 'e']

# You can remove items
l1.remove('b') # l1 = ['a', 'c', 'd', 'e']

# Pop removes and returns the last item in the list
l1.pop() # 'e', l1 = ['a', 'c', 'd']
# pop(i) removes and returns an element at position i

# Sort is a breeze
l2 = [7, 0.5, 23, 9]
l2.sort() # l2 = [0.5, 7, 9, 23]

# As well as reversing
l2.reverse() # l2 = [23, 9, 7, 0.5]

```

## Fun With Indices
You can do really cool things with strings and lists in Python. Recall how to
access a single element of a list `example_list_or_string[4]`. Well we can slice
the list or string in various ways. 

```python
fruits = ['banana', 'mango', 'tomato', 'plum', 'guava']
# Yes tomatoes are fruits, good grief

# Let's get all but the first fruit
fruits[1:] # ['mango', 'tomato', 'plum', 'guava']

# All but the last fruit
fruits[:4] # ['banana', 'mango', 'tomato', 'plum']

# Let's get every other fruit i.e. skip mango and plum
fruits[::2] # ['banana', 'tomato', 'guava']

# So there we go with the slicing: list_or_string[start:end:step]
# If nothing is put for start it defaults to begining of the list
# End defaults to the end (this felt too obvious) and step defaults to 1
fruits += ['sapodilla', 'cantaloupe', 'breadfruit', 'ackee', 'soursop']

# Let's get every other fruit from mango till breadfruit
fruits[1:8:2] # ['mango', 'plum', 'sapodilla', 'breadfruit']

# Start at the index of the first item you want
# End at the index of the last item you want plus 1
# Step in the name of love

# You can use negative indices here as well
fruits[-5:-1] # ['sapodilla', 'cantaloupe', 'breadfruit', 'ackee']
fruits[4:-2] # ['guava', 'sapodilla', 'cantaloupe', 'breadfruit']
# Think about why the above works!

# How to reverse a list in Python the awesome way?
fruits[::-1]

# Don't forget this also applies to strings!
mvp = 'LeBron James'
mvp[:5] # LeBro
mvp[::-1] # 'semaJ norBeL'
```

## Length
List and string length can be derived from the len function
```python
len(fruits) # 10
len(mvp) # 12
```

# Tuples
These are immutable collection of items that are encapsulated by parentheses
```python
x_coordinate = (4, 9)
# Access them by [] like with strings and lists
x_coordinate[0] # 4

# They can contain various types of data
character = ('mario mario', 25, ['super mario', 'mario galaxy', 'mario kart'])

# And can be nested as well
line_coordinates = ((-6, 3), (-18, 9))

# You can add elements to tuples
x_o = ('x',) # So a tuple with a single element needs to trailing comma
# There really is no purpose for a tuple with a single element -_-
x_o += ('o',) # ('x', 'o')
```

Wait a minute, tuples are immutable so why are we changing them? Well the + 
operator is actually creating a new tuple. So this is a new object all together,
the object reference for ('x',) is still intact. Let's also consider the
following
```python
spell_it_out = (3, ['one', 'two', 'three'])
spell_it_out[0] = 5 # TypeError, can't change the first number to anything else
spell_it_out[1].append('four') # Works
```

We get an error for trying to change the number because numbers are immutable 
objects. Lists on the other hand are mutable objects. So we can modify the list
without affecting the list's object reference. 

# Dictionaries
A dictionary is an unordered collection of key value pairs. Keys must be unique
in a dictionary and can be any immutable value (actually, the key should be
hashable - all built-in immutable objects are thankfully). Dictionaries 
themselves are mutable.

```python
# Movie ratings out of 10
movie_ratings = {
    'transformers': -10,
    'logan': 8.5,
    'assasin creed': '4.5',
    'fate of the furious': '2'
}

# We use [] to access elements as well
movie_ratings['logan'] # 8.5

# We can just as easily change values
movie_ratings['transformers'] = -20

# We can get all the keys from the dictionary
movie_ratings.keys() # Returns dict_keys object

# You may want the keys as a list, simply convert it
list(movie_ratings.keys())

# Extracting all the values is just as easy:
movie_ratings.values() # Returns dict_values object
list(movie_ratings.values())

# To find out if in an key is in a dictionary use the in keyword
'logan' in movie_ratings # True
'titanic' in movie_ratings # False
```

# If-Elif-Else

# For loop

# While loop

# List Comprehensions

# Lambda, Map and Filter

# Functions

# Classes and Objects
