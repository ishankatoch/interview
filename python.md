# Python Interview Questions

Below are some set of questions that can be considered for evaluation.

## Basics
> Is python interprted or compiled? Or both?

In the simple model of the world, “compile” means to convert a program in a high-level language into a binary executable full of machine code (CPU instructions). When you compile a C program, this is what happens. The result is a file that your operating system can run for you. it has machine level instructions . On the other hand , “interpreted” means to executing a program/source code line by line , one line at a time .

Considering from a general perspective , compiling is a taking a program in one language and converting it to another language , not necessarily machine code . In python , the source code is compiled to a much simpler form called bytecode . The bytecode instructions are similar to the CPU instructions but are executed by a virtual machine . The dis module in the Python standard library is the disassembler that can show you Python bytecode.

The catch is although the source code gets “compiled” to the bytecode but the process is entirely implicit . One never needs to invoke compiler to run a .py file. Another feature which points to the interpretable nature of python is the interactive prompt. One can run any code statement directly without explicitly converting it to the bytecode.

There are some building tools which can convert the python source code to executables , that automatically sets things up so that modules are imported from the ZIP archive containing PY or PYC(or PYO) files and use a small bootstrap script to add the ZIP archive to PATH . Examples include : Gordon McMillan’s installer (alternative download) (cross-platform), Thomas Heller’s py2exe (Windows), Anthony Tuininga’s cx_Freeze (cross-platform), or Bob Ippolito’s py2app (Mac).

**Another explaination**

During compilation, the entire source code is converted into machine code. Machine code is understandable by the CPU. The program will be executed only if the entire code is compiled successfully.

In interpretation, the code is executed line by line. Each line of source code in Python is translated into machine code during the execution. There is a Virtual Machine available to interpret the python code. The compilation and interpretation runtime structure is given in the above diagram.


> What is meant by dynamicaly typed language?

We need not define what type of value a variable will hold. The type will be assigned on runtime by checking what value it stores, like int, str, list, tuple, etc

It is one of the behaviors of high level programming language to check the type of data stored in a variable during the execution. In programming languages such as C, we must declare the type of data before using it.

> What is string slicing?

String slicing is the process of making subsets from strings. We can pass a range in the following syntax to slice the string.

Syntax: ```string[start:end:step]```

Consider the string “Hello World”. We can slice the string using the range values. To print ‘Hello’ from the string. Our range should be 0 to 5. The slicing creates sub string from start index to end-1 th index.

```python
string = "Hello World"   
print(string[0:5:1])   
print(string[6:11:1])

#Hello
#world
```


> What is python virtual environment?

Used create a separate runtime environment so  that we can keep dependancies of different project separated. Some project might need different python version of might need different version of libraries. Also helps to keep gloabal installation clean.

```python
python -m venv venv
source venv/bin/activate/
pip install flask
pip freeze > requirements.txt
pip install requirements.txt
deactivate
```

> Explain different data types in python?

int, float, str, list, tuple, dict, sets

> What is a lambda expression in python

Lambda is an anonymous function that helps us to create functions in single line of code. This is an important thing in functional programming. The lambda function should contains only one expressions in it.

Syntax: ```lambda arguments : expression```

```python
y = lambda x : x * 2
print(y(7))
#14
```

> Explain difference between list and tuple

- basic syntax [] and ()
- mutable and non-mutable
- can ask questions like t= (1,2,3) and t[1] =5. Will fail because tuple does not support item re-assignment

> What is range builtin function?

In Python you can use the range built-in to generate a sequence of numbers
```python
# range = iterable / lazy 
>>> range(1, 11) 
range(1, 11) 
# so casting to list 
# also note upper bound is exclusive 
>>> list(range(1, 11)) 
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 
# 3rd arg = stepping 
>>> list(range(1, 11, 2)) 
[1, 3, 5, 7, 9] 
# reverse 
>>> list(range(11, 1)) 
[] 
# use negative step 
>>> list(range(11, 1, -1)) 
[11, 10, 9, 8, 7, 6, 5, 4, 3, 2]
```

> What is enumerate in python? How can you print index inside a loop?

If you need the index inside a loop in Python use enumerate: 

```python
>>> names = 'bob julian tim sara'.split() 
>>> for i, name in enumerate(names, start=1): 
...     print(i, name) 
1 bob 
2 julian 
3 tim 
4 sara
```

> Sorted / min / max key argument

In Python, the ***sorted / min / max*** builtin functions take an optional ***"key"*** keyword argument that receives a callable:

```python
>>> ages = {'bob': 23, 'julian': 11, 'tim': 7, 'sara': 37} 
>>> sorted(ages.items()) 
[('bob', 23), ('julian', 11), ('sara', 37), ('tim', 7)] 
>>> sorted(ages.items(), key=lambda x: x[1]) 
[('tim', 7), ('julian', 11), ('bob', 23), ('sara', 37)] 
>>> sorted(ages.items(), key=lambda x: x[1], reverse=True) 
[('sara', 37), ('bob', 23), ('julian', 11), ('tim', 7)]
```

```python
ages = {'bob': 23, 'julian': 11, 'tim': 7, 'sara': 37}
sorted(ages, key=lambda x: ages[x], reverse=True)
['sara', 'bob', 'julian', 'tim']
```

```python
max(ages)
Out[24]: 'tim'
max(ages, key=lambda x : ages[x])
Out[25]: 'sara'
```

```python
>>> names = 'bob Julian tim sara'.split() 
>>> sorted(names) 
['Julian', 'bob', 'sara', 'tim'] 
>>> sorted(names, key=str.lower) 
['bob', 'Julian', 'sara', 'tim']
```

> Is vs == (object equality)

The difference in Python between comparing objects and their values:
```python
>>> a = [1, 2, 3]
>>> b = [1, 2, 3]
>>> c = a
>>> a == b # same content
True
>>> a == c # also same content
True
>>> a is c # same object
True
>>> a is b # not the same object
False
# to check for equal objects you can check their
# identity using id()
>>> id(a), id(b), id(c)
(140611808855040, 140611819909632, 140611808855040)
```

> F-strings

Starting Python 3.6 you can use f-strings.
F-strings let you embed variables and even expressions. More explicit and concise.

```python
for i in range(5):
    print(f'{i} is {"even" if  i %2==0 else "odd"}')
    
0 is even
1 is odd
2 is even
3 is odd
4 is even

```

> Collections.Counter

For counting in Python look no further than collections.Counter. Counter() can receive an iterable, a mapping or keyword args (nice!) most_common is useful to get, well, the most common elements.

```python
>>> from collections import Counter 
>>> languages = 'Python Java Perl Python JS C++ JS Python'.split() 
>>> Counter(languages) 
Counter({'Python': 3, 'JS': 2, 'Java': 1, 'Perl': 1, 'C++': 1}) 
>>> Counter(languages).most_common(2) 
[('Python', 3), ('JS', 2)]
```

```python
from collections import Counter
balls = ['blue','black','red','blue','black', 'red', 'red', 'red', 'black']
Counter(balls)
Out[31]: Counter({'blue': 2, 'black': 3, 'red': 4})
Counter(balls).most_common(2)
Out[32]: [('red', 4), ('black', 3)]
```
> Deduplicate values using a set

Need unique values from a list in Python? Use a set. Python has a basic data type called set which is an unordered collection with no duplicate elements. As they are implemented using hash tables, membership checking is fast. The other use case is eliminating duplicate entries.
```python
 >>> languages = 'Python Java Perl PHP Python JS C++ JS Python Ruby'.split() 
 >>> set(languages) 
 {'Perl', 'JS', 'Python', 'Ruby', 'Java', 'PHP', 'C++'}
```
> List comprehension to filter out values

Use a list comprehension in Python to filter a list: 
```python
>>> languages = ['Python', 'Java', 'Perl', 'PHP', 'Python', 'JS', 'C++', 'JS', 'Python', 'Ruby'] 
>>> [l for l in languages if l.lower().startswith('p')] 
['Python', 'Perl', 'PHP', 'Python', 'Python'] # alternative but less readable 
>>> list(filter(lambda l: l.lower().startswith('p'), languages)) 
['Python', 'Perl', 'PHP', 'Python', 'Python']
```
> Any / all built-ins 

A Pythonic way to check if any / all elements of an iterable are true. 
```python
>>> languages = ['Java', 'Perl', 'PHP', 'Python', 'JS', 'C++', 'JS', 'Ruby'] 
>>> all(len(l) >= 2 for l in languages) 
True 
>>> any('++' in l for l in languages) 
True
```

> Join strings

Use join in Python to combine a list of multiple strings: 
```python
>>> tweets = ("I was happy with the book", "this is awful", ... "Python is object oriented", "Python is awesome") 
>>> print('\n'.join(tweets)) I was happy with the book this is awful Python is object oriented Python is awesome 
>>> print(' >> '.join(tweets)) I was happy with the book >> this is awful >> Python is object oriented >> Python is awesome 
```
***can be good question to ask***
```python
# make sure all elements are strings 
>>> '-'.join([100, 'pybites', 'tips', 4, 'you']) 
Traceback (most recent call last): File "<stdin>", line 1, in <module> TypeError: sequence item 0: expected str instance, int found 
>>> '-'.join(str(w) for w in [100, 'pybites', 'tips', 4, 'you']) 
'100-pybites-tips-4-you'
```
join is a string method, so you call it on the string you want to use to concatenate the elements in the iterable you pass into it. Make sure all these elements are strings or you'll hit a TypeError. Also note that this can be significantly faster than ordinary string concatenation if you have a lot of strings!

> Reverse a list

Different ways to reverse a list in Python: 

The first example modifies numbers in place, reversed returns a list_reverseiterator iterator which we cast to a list to show in the REPL (the original list remains unchanged). Lastly, using a negative step in the list slicing syntax returns a new object as well.

```python
>>> numbers = [1, 2, 3, 4, 5] 
# in-place 
>>> numbers.reverse() 
>>> numbers [5, 4, 3, 2, 1] 
>>> list(reversed(numbers)) 
[1, 2, 3, 4, 5] 
>>> numbers 
[5, 4, 3, 2, 1] 
>>> numbers[::-1] 
[1, 2, 3, 4, 5]
```

> Which python version do you use? How to check it?

python -V

> Open a file sample.txt for wirting and write "Hello world" in it or Prevent overwriting files?

```python
with open('sample.txt','w') as f:
    f.write('Hello world')
```

```python
#Python's open built-in has the 'x' switch which opens the file for "exclusive creation", failing if the file already exists.
>>> with open('hello', 'x') as f: 
...     f.write('spam') 
... Traceback (most recent call last): File "<stdin>", line 1, in <module> FileExistsError: [Errno 17] File exists: 'hello'
```

> Is it faster to search a list or a dictionary in Python?

Searching in a list can be considerably slow as compared to a dictionary. The effect is even more pronounced , when the size of elements to search increases . As a fact, using a dictionary is over 100,000x faster than using a list if the search is on 10 million items. So , why is list slow as compared to a dictionary ? The reason is simple , the list uses iterative method to search for an element while a dictionary uses a hash lookup

> What are Iterators in Python?

The objects in python that implements the iterator protocols are called iterators. iter is the keyword used to create the iterable objects. It iterates throough various iterable objects such as List, dictionary.

```python
my_list = [1, 2, 3, 4, 5]   
my_iterator = iter(my_list)
print(next(my_iterator))   
print(next(my_iterator))   
print(next(my_iterator))
#output
1   
2   
3
```

> How to generate random numbers in Python?

There is no in-bulit function in python to generate random numbers We can use random module for this purpose. We can create random number from a range or list. randint is the simple method used to create a random number between two numbers.

```python
import random   
print( random.randint(0,9))
```

>  How to create private data in Python?

Protected members can be accessed only by the class and its sub classes. The following code examples shows that how the private and public members works in python.

```python
class emp:   
    def __init__(self, s):   
        self.__salary = s   
t = emp(25000)   
print(t.__salary)
#output
# Traceback (most recent call last):   
#   File "main.py", line 5, in <module>   
#     print(t.__salary)   
# AttributeError: 'emp' object has no attribute '__salary'
```

> What is the meaning of this commonly used statement in Python If \_\_name\_\_ == "\_\__main\_\_"


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

> Decorators
- syntax
- use cases
- give me a decorator to print all args before running or time it function

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args,**kwargs):
        print('Before function call ',func.__name__)
        func(*args,**kwargs)
        print('After function call ', func.__name__)
    return wrapper
```

> Generators

> Unit Testing

> Logging module, configuration etc

> Types of argument positional, keyword, *args, **kwargs

> Exception handling in python. try, catch, finally

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

> Use of with statement
- exception handling
- make code clean and readable
- e.g file streams and databases

> WAP to check if number is palindrome

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

> have you used any third party libraries, name them and how they were used.

> How can you use regular expression in python

import re
what are re, metacharacters

`^$?+*.[]{}

> Explain inheritance in python

- example
- super()
- types
- instance method, class method, static method

> WAP to find largest word in a text file
- words = read.split()
- max (word, key=len(word))

> WAP to count frequency of words ina file

- Counter(f.read().split())