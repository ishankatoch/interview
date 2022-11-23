# Python Interview Questions

> Which version of python you last worked upon?

> Which IDE you use for Python Development? Any extensions you are using?

> How do I modify a string?

```python
s = 'abc'
s[2] = 'd'
Traceback (most recent call last):
  File "<input>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

You can’t, because strings are immutable. In most situations, you should simply construct a new string from the various parts you want to assemble it from.

_immutable_
None
bool
int
float
str
tuple

_mutable_
list
dict
set

mutable also means unhashable

> Give syntax for a lambda function for function which will give output like

y(1,3) #sum of arguments and 10

14

```python
y = lambda x,y : x + y + 10
```

> I have a list of cars. How will you sort this in a reverse order of year?

```python
cars = [
  {'car': 'Ford', 'year': 2005},
  {'car': 'Mitsubishi', 'year': 2000},
  {'car': 'BMW', 'year': 2019},
  {'car': 'VW', 'year': 2011}
]
```

sorted(cars, key=lambda x: x['year'], reverse=True)

> Is vs == in OOP

```python
class Employee:
    def __init__(self, name):
        self.name = name
    #
    # def __eq__(self, other):
    #     return self.name == other.name


e1 = Employee('Naba')
e2 = Employee('Naba')

print(f'e1 ==e2: {e1 == e2}')
print(f'e1 is e2: {e1 is e2}')
```

#Explain the results

> Shallow copy and deep copy

- A shallow copy constructs a new compound object and then (to the extent possible) inserts references into it to the objects found in the original.
- A deep copy constructs a new compound object and then, recursively, inserts copies into it of the objects found in the original
- making a shallow copy of a nested object with copy (or using slicing: [:]) inner objects are references, so updating one updates all copies. Not so with deepcopy.

````python
items = { 'id': 1, 'name':'laptop'}
items_copy = items
items_copy['name'] = 'Desktop'
items
#output oops it should have stayed intact
{'id': 1, 'name': 'Desktop'}
#using deepcopy
items = { 'id': 1, 'name':'laptop'}
items_copy = deepcopy(items)
items_copy['name'] = 'Desktop'
items
{'id': 1, 'name': 'laptop'}

> Explain the below code

```python
def func(sample_list=[]):
    sample_list.append(12)
    # print(id(sample_list))
    return sample_list

print(func()) # [12]
print(func()) # [12,12]
````

Since list is mutualable type of data structure, the first time func is called, the list is empty, but when the same function is called twice, the list already has an item. We cans sure of the that by printing the id of the sample_list used in the first, on each subsquent call to the function, the id will return the same value.

> What are Decorators in Python?

A decorator is any callable Python object that is used to modify a function, method or class definition. Decorators allow us to wrap another function in order to extend the behavior of wrapped function, without permanently modifying it.

Always use wraps on your decorators to preserve your function's meta data (e.g. docstring).

```python
from functools import wraps
from time import time, sleep


def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time()
        result = func(*args, **kwargs)
        end = time()
        print(f'Elapsed time {func.__name__}: {end - start}')
        return result
    return wrapper


@my_decorator
def my_func(name):
    sleep(2)
    print(f'My name is: {name}')


my_func('ishan')

```

> How to chain decorators?

```python
def make_bold(fn):
    def wrapped():
        return "<b>" + fn() + "</b>"
    return wrapped

def make_italic(fn):
    def wrapped():
        return "<i>" + fn() + "</i>"
    return wrapped

@make_bold
@make_italic
def index():
    return "hello world"

print(index())
## returns "<b><i>hello world</i></b>"
```

> Create a function which can add any number of arguments

```python
def add_unknown(*args):
...     sum=0
...     for arg in args:
...         sum+=arg
...     return sum
...
add_unknown(1,4,2,5,8)
20
```

> List comprehensions

```python
nums = [1,2,3,4,5]

#square
[ num * num for num in nums]

#cube of even nums

[n*n*n for n in nums if n%2==0]

#dictionary
{n:n*n for n in nums if n%2==0}

```

> What is GIl/

The Global Interpreter Lock (GIL). CPython (the most common Python implementation) is not fully thread safe. In order to support multi-threaded Python programs, CPython provides a global lock that must be held by the current thread before it can safely access Python objects. As a result, no matter how many threads or processors are present, only one thread is ever being executed at any given time. In comparison, it is worth noting that the PyPy implementation discussed earlier in this article provides a stackless mode that supports micro-threads for massive concurrency.

> What is difference between from pacakge import \* and import package?

Generally when we do from module import _ all the functions and varaibles from that module gets imported to the namespace. But in case of packages it is not the case, infact from package import _ has no impact at all. If we want to use our package in this case then we will have to use **init**.py file and define the functions and varaibles in the **all** variable. Then whenver we say from pacakge import \* then everything mentioned under **all** varaiable gets imported.

For import package everythin mentioned under **init**.py gets imported in current namespace.

> Explain the UnboundLocalError exception and how to avoid it?

What will be output of below statement

```python
>>> x = 10
>>> def foo():
...     print(x)
...     x += 1

>>> foo()
```

Output

```python
>>> foo()
Traceback (most recent call last):
...
UnboundLocalError: local variable 'x' referenced before assignment
```

When you make an assignment to a variable in a scope, that variable becomes local to that scope and shadows any similarly named variable in the outer scope. Since the last statement in foo assigns a new value to x, the compiler recognizes it as a local variable. Consequently when the earlier print(x) attempts to print the uninitialized local variable and an error results.

In the example above you can access the outer scope variable by declaring it global:

```python
>>> x = 10
>>> def foobar():
...     global x
...     print(x)
...     x += 1
>>> foobar()
10
```

> What are Python genrators?

Python Generator functions allow you to declare a function that behaves likes an iterator, allowing programmers to make
an iterator in a fast, easy, and clean way. An iterator is an object that can be iterated or looped upon. It is used to
abstract a container of data to make it behave like an iterable object. Examples of iterable objects that are used more
commonly include lists, dictionaries, and strings.

Python generators are a simple way of implementing iterators.

_so why use generator -> because of memory consumption_

```python
lst = [i for i in range(10001)]
g = (i for i in range(10001))
import sys
print(sys.getsizeof(lst))
print(sys.getsizeof(g))
85176
112
```

_Use Cases_
so if you need to loop over lots of lots of data then probably use a gnerator
you can also use generator if you dont need to evaluate all the values at once

for eg [slow_method(i) for in range(1001)] this will evaluate all at once
on the other hand (slow_method(i) for i in range(1001))

generator function -> a function that returns a generator. uses yield instead of return
any fucntion can be generator if it uses yield.
yield is like next, except when you call next o this generator it will resume where it left off

Difference Between Generator Functions and Regular Functions
The main difference between a regular function and generator functions is that the state of generator functions are
maintained through the use of the keyword yield and works much like using return, but it has some important
differences. the difference is that yield saves the state of the function. The next time the function is called,
execution continues from where it left off, with the same variable values it had before yielding, whereas the return
statement terminates the function completely. Another difference is that generator functions don’t even run a
function, it only creates and returns a generator object. Lastly, the code in generator functions only execute
when next() is called on the generator object.

```
def f():
    yield 1
    yield 2
    yield 3


g = f()  # generator object

print(next(g))
print(next(g))
print(next(g))
```

> What is the meaning of this commonly used statement in Python If \_\_name\_\_ == "\_\_\_main\_\_"

It's used at the end of a script to write code that ONLY executes if the module (script) is called directly. Code in this if does NOT run when the module gets imported into another module or in the REPL.

```python
$ more script.py
def func():
    print("Hello from function")
if __name__ == "__main__":
    func()
# main block gets invoked
$ python script.py
# Hello from function
$ python
>>> import script # main block does not get invoked
>>> script.func() Hello from function
```

Also "\_\_name\_\_" has value of `__main__` when the script is invoked directly otherwise it will have the name of the module.
Not to be run in cae of imports.

> How would you parse user argument in a python script

```python
# groups.py
import argparse

my_parser = argparse.ArgumentParser()
my_group = my_parser.add_mutually_exclusive_group(required=True)

my_group.add_argument('-v', '--verbose', action='store_true')
my_group.add_argument('-s', '--silent', action='store_true')
my_group.add_argument('-d', '--debug', action='store_true')

my_group_2 = my_parser.add_argument_group()
my_group_2.add_argument('-r', '--rerun',action='store')
my_group_2.add_argument('-t','--run-history',action='store')

args = my_parser.parse_args()

print(vars(args))
```

> What are different ways yo achieve multithreading in Python
``` python
import concurrent.futures
import urllib.request

URLS = ['http://www.foxnews.com/',
        'http://www.cnn.com/',
        'http://europe.wsj.com/',
        'http://www.bbc.co.uk/',
        'http://some-made-up-domain.com/']


# Retrieve a single page and report the URL and contents
def load_url(url, timeout):
    with urllib.request.urlopen(url, timeout=timeout) as conn:
        return conn.read()


# We can use a with statement to ensure threads are cleaned up promptly
with concurrent.futures.ThreadPoolExecutor(max_workers=5) as executor:
    # Start the load operations and mark each future with its URL
    future_to_url = {executor.submit(load_url, url, 60): url for url in URLS}
    print(future_to_url)
    for future in concurrent.futures.as_completed(future_to_url):
        url = future_to_url[future]
        try:
            data = future.result()
        except Exception as exc:
            print('%r generated an exception: %s' % (url, exc))
        else:
            print('%r page is %d bytes' % (url, len(data)))
```            
