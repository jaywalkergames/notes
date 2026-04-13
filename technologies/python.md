# How does a Python program work

A Python program begins its execution at the ***main***() function.

# Python's Object-Oriented Structure

All data in a Python program is represented by objects or relations between objects. Each object has an id (address in memory) and a type (definition of what values can be stored in the object). Mutable objects can change their value (dictionaries, lists) and Immutable objects cannot (numbers, strings, tuples). Containers are objects contain references to other objects. A mutable object reference by an immutable container can still change its value. When an object becomes unreachable it may become garbage collected.

# How to write good Python

## Create Virtual Environment

```
create: python3 -m venv env
activate: source env/bin/activate
deactivate: deactivate
show requirements: pip freeze
install requirements: pip install -r requirements.txt
```

## Styling

- Use Flake8 extension to catch style issues
- Use isort extension to sort imports
- Use 4 space indentation
- Comments should be complete sentences.
- Place module level dunders directly after module docstring
- Modules declare names in public API using
- Only use lambdas inline
- Be specific with exceptions (no base exception clause)
- Always return ‘None’ when returning expression in other block
- Compare object types with isinstance()
- Use trailing comma for multiline literals and single element tuples
- Always define constants on modular level
- Use self for first arg of instance methods and cls for first arg of class methods
- Use is operator for references or singletons only
- Always close resources using try...finally or with for optimal gc

## Naming

- Modules: shortalllower
- Functions, variables, files: snake_case
- Classes: CamelCase
- Methods: snake_case for public, _snake_case for private
- Exceptions: CamelCaseError
- Constants: UPPER_SNAKE

## Docstrings

- Docstrings have a summary line, blank line, description
- Write docstrings for all public modules, functions, classes, and methods
- Docstring for a script should be usable as its "usage" message
- Should document the scripts function, command line syntax, variables, files
- Should be printed when the script is invoked with incorrect args (or with -h)
- Docstring of a module should list the classes, exceptions, functions, and objects exported. It should give a one line summary of each Docstring for a package's \_\_init__.py module should list the modules and subpackages exported
- Docstring for a function or method should summaraize its behavior. It should document its arguments, return values, exceptions, restrictions, and whether keyword arguments are a part of its interface
- Docstring for a class should summarize its behavior. It should list public methods and instance variables, list additional interfaces for subclasses separately. If inherited, a class should summarize this use. "Override" to indicate a subclass method replaces a superclass method. "Extend" to indicate a subclass method calls a superclass method. Class constructored documented in its \_\_init__ method

# How to write efficient Python programs?

## Run optimizations

- -O removes asserts,
- -OO removes asserts and docstrings
- Use compileall module to create .pyc files of all modules in a directory (faster loading)
- Numba

## timeit

```python
import timeit

total_time = timeit.timeit('test_function(args)', globals=globals(), number=execute_amount)

```

## cProfile

```python
import cProfile

cProfile.run(test_function(args))

# Creating profile object
ob = cProfile.Profile()
ob.enable()

# As you increase the power time will increase
# as per your machine efficiency.
num = 18**200000

ob.disable()
sec = io.StringIO()
sortby = SortKey.CUMULATIVE
ps = pstats.Stats(ob, stream=sec).sort_stats(sortby)
ps.print_stats()

print(sec.getvalue())

```

# Functions

```python
# A defined function block
def defined_function(my_arg):
    return my_arg > 0

# Define a list
my_list = [-1, 0, 1, 2]

# Filter Map Function
my_list[:] = filter(defined_function, my_list)

# Filter list comprehension
my_list[:] = [x for x in my_list if x > 0]

# Create 5x10 list with list comprehension
A = [[None] * 5 for i in range(10)]
```

# Objects

```python
class MyClass:

    # Bettern to implement module-level functions than static methods
    # Static variable count is shared amongst all objects of class
    count = 0

    def __init__(self, data):
        MyClass.count += 1
        self.data = data
        self.index = len(data)

    def __iter__(self):
        """Creates an iterable class"""
        return self

    def __next__(self):
        """Defines how to iterate class (reverse in this case)"""
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]

    def my_method(self):
        print("Hello World")

class MyDerived(MyClass):
    def my_method(self):
        """Calls MyClass.my_method()"""
        super().my_method()

# Creating reverse generator (yield returns data, resumes when next() called)
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]

inherited_object = MyDerived([1, 2, 3])
if issubclass(MyDerived, MyClass) and isinstance(inherited_object, MyClass):
    inherited_object.my_method()

# Print elements in original order
for i in inherited_object:
    print(i)
```

# Types

```python
import heapq
from enum import Enum, unique
from collections import Counter, OrderedDict, deque

def none_type():
    """None signifies the absence of a value (bool value is False)"""
    return None

def bool_type():
    """Bools can be True or False"""
    return True

def int_type():
    """Ints are any integer"""
    return 2

def float_type():
    """Floats are any double precision floating point number"""
    return 3.14159

def complex_type():
    """Complex are any complex numbers (pair of floats .real and .imag)"""
    return complex(2.5, 2.5)

def sequence_types(seq):
    """Sequences are tfinite ordered sets indexed by nonegative numbers.

    Slicing: a[i:j:k] where i is start index, j-1 is end index, k is step size
    len(): returns number of elements in sequence O(1)

    Iteration: for i in range(seq)
    Reveresed: for i in reversed(seq)
    Indexed: for i in range(len(seq))
    """
    return seq[2, 9, 3]

def string_type():
    """Strings are immutable sequences of Unicode points

    Creation: "", ''
    Get: O(1)
    """
    return "Hello World"

def tuple_type():
    """Tuples are immutable sequences of Python objects

    Creation: (), (a,), or m(a, b, c) literals
    Get: O(1)
    """
    return (1, 2, 3)

def list_type():
    """Lists are mutable sequences of Python objects

    Creation: []
    Append: O(1)
    Pop: O(1)
    Remove: O(n)
    Insert: O(n)
    Get: O(1)
    Set: O(1)
    Slice: O(k)
    Set Slice: O(k+n)
    x in s: O(n)
    min: O(n)
    max: O(n)
    """
    return [1, 2, 3]

def dict_type():
    """Dicts are mutable finite sets of objects indexed by arbitrary values

    Creation: {a: b, c: d}
    Get: O(1) amortized
    Set: O(1) amortized
    Remove: O(1) amortized
    k in d: O(1) amortized
    """
    my_dict = {"Hello": "World", "Goodbye": "World"}
    return my_dict["Hello"]

def set_type():
    """Sets are mutable, unordered, finite sets of unique objects

    Creation: set(a, b)
    x in s: O(1)
    Union: O(n+m)
    Intersections: O(min(n, m))
    Difference (s-t): O(n)
    """
    return set(1, 1, 2)

def frozenset_type():
    """Frozen sets are immutable, unordered, finite set of unique objects

    Creation:  frozenset()
    x in s: O(1)
    Union: O(n+m)
    Intersections: O(min(n, m))
    Difference (s-t): O(n)
    """
    return frozenset(1, 1, 2)

def heapq_type():
    """Priority Queue
    
    Creation: heapq.heapify(my_list)
    Add: heapq.heappush(my_list, element)
    """
    return heapq.heapify([1, 5, 7, 9, 3])

def deque_type():
    """Double-ended queue (doubly linked-list)

    Creation: "", ''
    Append: O(1)
    Appendleft: O(1)
    Pop: O(1)
    Popleft: O(1)
    Remove: O(n)
    Get: O(n)
    """
    return deque(1, 2, 3)

def enum_type():
		"""Set of names bound to unique values"""
		@unique
		class Color(Enum):
			RED = 1
			GREEN = 2
			BLUE = 3
		return Color.RED

def ordered_dict_type():
    """Dict that tracks a list of the ordering of insertions"""
    my_ordered_dict = OrderedDict({"Hello": "World", "Goodbye": "World"})
    return my_ordered_dict[0]

def counter_type():
    """Dict that count the number of each iteration in a sequence"""
    my_counter = Counter("alabama")
    return my_counter['a']

def type_conversions():

    # int()
    int("123")  # O()
    int(3.5)    # O()
    int(0b101)  # O()
    int(0x1b3)  # O()

    # float()
    float(3)
    float("3.14")

    # str()
    str(123)
    str(3.14)

    # list()
    list((1, 2, 3))
    list(set(1, 1, 2))

    # tuple()
    tuple([1, 2, 3])
    tuple(set(1, 1, 2))

    # set()
    set([1, 2, 3])
    set((1, 2, 3))
```

```python
# Type Hints
def moon_weight(earth_weight: float) -> str:
    return f'On the moon, you would weigh {earth_weight * 0.166} kilograms.'

# Type Aliases
type ConnectionOptions = dict[str, str]
type Address = tuple[str, int]
type Server = tuple[Address, ConnectionOptions]

# types
from collections.abc
from typing import Union, Optional, 
```

# Tips

```python
from sys import stdin, stdout

# Fast IO
stdin = open('input.txt', 'r')
stdin.readline()
stdout.write("Hello World")

def concatenate_strings(my_strings):
    """Create one string given a list of strings"""
    return ''.join(my_strings)

def check_prefix(my_string, prefix):
    """Check if my_string begins with prefix"""
    return my_string.startswith(prefix)

def check_suffix(my_string, suffix):
    """Check if my_string ends with suffix"""
    return my_string.endswith(suffix)

# Custom with context operator
class CustomOpen(object):
    def __init__(self, filename):
        self.file = open(filename)

    def __enter__(self):
        return self.file

    def __exit__(self, ctx_type, ctx_value, ctx_traceback):
        self.file.close()
with CustomOpen('file') as f:
    contents = f.read()

# another custome with contect operator
from contextlib import contextmanager
@contextmanager
def custom_open(filename):
    f = open(filename)
    try:
        yield f
    finally:
        f.close()
with custom_open('file') as f:
    contents = f.read()

# how decorators work
def foo():
    # do something
def decorator(func):
    # manipulate func
    return func
foo = decorator(foo)  # Manually decorate
@decorator
def bar():
    # Do something
# bar() is decorated

# create a n-sized list of the same things
four_nones = [None] * 4

# use requests lib
```
