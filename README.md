# Python 3

* Table of contents
[[_TOC_]]

## Conda
1. create from yml: conda env create -f environment.yml

## Fantastic Resources:
https://elitedatascience.com/python-cheat-sheet
https://regex101.com
https://hector.dev/2020/12/29/validating-data-in-python-with-cerberus.html
http://blog.cleverelephant.ca/writings
http://www.sqlrun.com

## Control Flow
### While Loops
```py
c = 5
while c != 0:
    print(c)
    c -= 1
```
### Break
```py
while True: #Infinite loop.
    response = input()
    if int(response) % 7 == 0:
        break
```
## Strings, Collections and Iterations
### Strings and String Literals
Be aware of escape functions. Use r (raw) if need be, ie. path = r"C:etc/etc/etc"
```py
/n #New line.
string = "This is a string with a /n new line"

string.capitalize() #One of type string's functions.
```
### List
```py
list = [3,4,"Daniel"]
list.append("rich")

list("Rich")
#returns ["r","i","c","h"]
```
### Dictionary
Dictionaries map keys to value
```py
d = {'daniel':37,'maike':29}
d['daniel'] #Returns 37
d['maike']=30 #Updates the value to 30 from 29
```
### Bytes
Bytes are like strings. b'string'. To change bytes to string
```py
from urllib.request import urlopen
story = urlopen('http://sixty-north.com/c/t.txt')
story_words = []
for line in story:
    line_words = line.decode('utf-8').split() #.decode('utf-8') will decode bytes to string.
    for word in line_words:
        story_words.append(word)
story.close()
story_words
```
## Modularity
### __name__
Python set the value of dunder name differently depending on how the module is being used (importing or executing). Use the following under the function in the .py file.
```py
if __name__ == '__main__':
    fetch_words()
```
It is best practice to define a module (a .py file) with this so it can be imported to the Python REPL without running immediately, as __name__ == '__name__' in REPL. Imported to a text editor __name__ == '__main__'.
## Objects and Types
1. Python uses dynamic typing, ie., you dont have to declare the type.
2. Pythin uses strong typing, ie., types are not coerced to match.
3. dir() will give a list of object attributes.
4. __name__ is the name of the object.
5. __doc__ is the doc string of the object.
6. Strings have a repitition operation, *. String * integer will return copies of the string.

To see if objects are equivalent, ie., have the same value:
```py
a == b
```
To see if objects have the same reference, ie., name tag, use:
```py
a is b
```
### Function Arguments and Defaults
Args with defaults must be list after args without defaults.
```py
def banner(message, border='-') # Border has a default set.
    line = border * len(message)
    print(line)
    print(message)
    print(line)
    
>>>banner('Norwegian Blue')
>>>--------------
   Norwegian Blue
   --------------
```
Positional arguments can be placed in the defined order without specifing a key. Alternatively, referring to above, one could call banner(border='*', message = 'New Zealand'). Keys must be placed AFTER any positional arguments.
#### Mutable Default Values
Default values are only called once, so a default list that has values added to it will inherit these when using the function again. Solution: only use IMMUTABLE default values! ..Such as integers and strings. Use None in place of a list if suitable:
```py
def add_spam(menu=None)
    if menu = None:
        menu = []
        menu.append('spam')
        return menu
```
### Type Systems
```py 
def add(a, b):
    return a + b
```
This will return a + b regardless of type, but will not add different types.
### Scopes
Names are looked up in the narrowest relevant context: The LEGB rule
1. Local
2. Enclosing
3. Global
4. Built in

Rebinding global names:
```py
count = 0
def set_count(c):
    global count
    count = c
def show_count()
    print(count)
```
By using global count, when setting the count with set_count, the global count, i.e., count = 0 will change.
### Everything is an object
This can be seen by using the type() function on anything.
## Built in Collections
### Tuples
Immutable. 
```py
t = (67, 'this is a tuple', 2)

t1 = (('this is a nested tuple', 16), (67, 'this is a tuple', 2))
t[1][2] # This indexing returns 2

t = (341,) # To create a single entry tuple you must set a comma.
t = () # Although, this is how to make an empty tuple (no comma).

t = 1,2,3,4,5,6 # Returns a tuple (1,2,3,4,5,6), ie., brackets can be omitted.

def minmax(items)
    return min(items), max(items) # Returns (min, max) in a tuple.
```
#### Tuple Unpacking!
```py
lower, upper = minmax([34, 45, 12, 56, 78]) # lower returns 12, upper returns 78

(a, (b, (c,d))) = (4, (3, (2,1))) # a returns 4, b returns 3 etc.
```
#### Tuple Swapping
```py
a = 'jelly'
b = 'bean'
a, b = b, a # a returns 'bean', b 'jelly'
```
#### Create Tuple
```py
tuple('Shane') # Returns ('S','h','a','n','e')
```
#### in not in
```py
5 in (3,4,5,6,7) # Returns True
5 not in (3,4,5,6,7) # Returns False
```
### Strings
```py
'new' + 'found' + 'land' # Returns 'newfoundland'
# Better to use join() on extensive concatenation as + methods creates lots of temporaries.

#join() can also:

colors = ';'.join(['#45ff23', '#2321fa']) # Returns '#45ff23 ; #2321fa'
name = ' '.join(['Shane', 'Daniel', 'Rich']) # Returns 'Shane Daniel Rich'
```
##### Partition
```py
'unforgetable'.partition('forget') # Returns ('un', 'forget', 'able')
# Is often used with unpacking
departure, seperator, arrival = 'London:Edinburgh'.partition(':') # departure returns 'London', etc.
departure, _, arrival = 'London:Edinburgh'.partition(':') # Convention is to use _ for unused or dummy values, some Pythons programs with look for these underscores.
```
##### format() and f strings
In f strings f is placed at before the start of the string.
```py
'The age of {0} is {1}. {0} is a {occ[0]}'.format('Jim', 24, occ=('pilot', 'banker'))

import math
'Math constants: pi={m.pi:.3f}, e={m.e:.3f}'.format(m=math) # Three decimal places :.3f

f'Math constants: pi={m.pi:.3f}, e={m.e:.3f}'

value = 4 * 20
f'The value is {value}.'
```
### range() and enumerate()
```py
for i in range(5):
range(5) # Retruns range(0,5), ie., type range.
list(range(0, 10, 2)) # Returns a list with a 2 step, [0,2,4,6,8]

# Enumerate places the values in tuples with the index.
t = [2, 3, 6, 76]
for i, v in enumerate(t): # Unpacking with enumerate.
    print(f'i = {i}, v = {v}')
```
### Lists
#### Negative indices
Ie., list[-1] or list[-2] will refer to the last and seconds last item in the list.
#### Slicing and Soft Copying
```py
a_list[start:stop]
list = [1,2,3,5]
print(list[2:]) # Returns [3,5]
# The below are soft copies, in that they create a copy of the references but the items mutated, for example with an append(). Rebinding, ie replacing the list will stop this. 
list2 = list[:] # Full slice. Where list is list2 is False but where list == list2, BUT, items are updated in both.
list2 = list.copy() # A more readable way to copy.
list2 = list(list) # Best way to copy, as any iterable series as a source can be passed, not just lists.
# See below:
list2 = [[9,8,7],[1,2,3]]
list5 = list2[:]
list5[1] = [99,88,77] # This rebinds and creates a new object in [1] that is not the same as list2.
list2[1].append(1000) # 1000 will therefore only be appended to list2[1]
list5[0].append(2000) # The object at [0] is still the same object in both lists, so an append of 2000 will appear in both lists.
print(list2)
print(list5)
```
#### index()
```py
w = 'the fox jumped over the dog'.split() # Returns a list of words split by a comma.
i = w.index('fox') # Searching through list for a match and returns index.
print(i)
w.count('the') # Returns 2
```
#### delete, del or remove() and insert(), extend()
```py
del list[0]
list.remove('fox')

list.insert(2, 'sheep') # Insert 'sheep' at index 2.
list.extent(['duck', 'bird']) # Adds these two items to the end of the list.
```
#### Rearranging a list, reverse(), sort() and sort(key=)
Reverse is self explanatory.
```py
list.sort(reverse=True) # Decending order. 
list.sort() # Default is acending order.
list.sort(key=len) # Sorts by length.
```
#### sorted() and reversed() 
1. They have the advantage of working on any finite iterable source object (ie., not just lists). 
2. sorted() create a new list object that is sorted, wheras reversed creates a list_reverseiterator object that can be converted to a list using the list() function.
```py
list = [1,2,6,8]
list2 = reversed(list) # Creates a list_reverseiterator object.
list(list2) # Create list and return [8,6,2,1]
```
### Dictionaries
Made of keys (immutable) and values (may be mutable, lists for example).
```py 
dict = {'Point': (23.4, 75.3), 'Linestring':(24.5, 24.7, 32.5)}
dict['Point'] # Returns (23.4, 75.3)
```
#### dict()
dict() can turn a list of tuples into a dictionary, or simply by passing with key=value
```py
list = [(23, 45), (2, 50), (46, 32)]
dict = dict(list)

phonectic = dict('a'='alfa', 'b'='bravo', 'c'='charlie')
```
#### Copying, with either .copy() or dict() 
See list above. As with list, copying is 'shallow', ie., only copies the references and the values will be updated in both unless rebound.

#### .update() , ie., add new entries or update. Add with augmented operator +=.
Use same key to override existing value.
```py
dict1 = {'Point': (23.4, 75.3), 'Linestring':(24.5, 24.7, 32.5)}
dict1.update({'Point':(10.1, 13.2)}) # Returns dict with updated values for 'Point'

dict1['Linestring'] += (45.8, 99.9, 100.1) # Adds these three floating point numbers to the three there.
dict1['Polygon'] = (45.8, 99.9, 100.1, 45.8) # Adds new entry to dictionary.
```
#### .keys() and .values()
Iterates over one or the other in a loop.
#### .items()
Iterates over keys and values in tandom. Yields a key, value tuple of each iteration.
```py
for key, value in dict.items():
    print(f'{key} => {value}')
 ```
 #### in, not in
 Work on the keys.
 ```py
 dict = {'Point': (23.4, 75.3), 'Linestring':(24.5, 24.7, 32.5)}
 'Point' not in dict # Returns False.
 ```
 #### del used to delete on keys
 ```py
 del dict['Point']
 ```
 #### from pprint import pprint as pp
 Gives an easier readability.

### Sets
1. Wheras an emply dictionary can be intaniated using emply curly braces, a set must use the command set. new_dic = {}. new_set = set().
2. Order is arbitrary is sets. This goes for iterating through it too. 
3. To add a single value to a set use the add() method. Adding an element that does not exist does nothing, neither will it produce an error.
4. update() can be used to add an iterable series of values.
5. in and not in work on sets. 
6. discard() or remove(), remove() will cause a key error if not present, discard() will not and just continue.
7. copy(), like other iterable series, will make a soft copy.
```py
new_set = {23, 12, 56, 24}
new_set = set([34, 12, 2, 2, 2, 56, 3]) # any iterable series can be sent to the set constuctor and duplicates are discarded! Handy way to remove ducplicates.
34 in new_set # Returns True
new_set.add(99)
new_set.update([34, 65, 21])
new_set.discard(65)
```
#### Set Algebra
```py
blue_eyes.union(blond_hair) # Returns all values that are in either and both sets.
blue_eyes.intersection(blond_hair) # Returns all values that are the same in both sets.
blond_hair.difference(blue_eyes) # Returns those with blond hair without blue eyes. 
blond_hair.semmetric_difference(blue_eyes) # Returns all values that exclusive in each set, ie., only blue eyes or blond hair and not both.
blond_hair.isubset(blue_eyes) # Do all those with blond hair have blue eyes?
.issuperset()
.isdisjoing()
```
### Protocols
A set of operations that a type must support to implement the protocol. In C# these need to be defined as interfaces or base classes but not in Python.
## Exceptions
1.Avoid type errors, they will occur of their own.
2. Python uses EAFP (easier to ask forgiveness than to ask permission). Try and accept to handle errors rather than trying to check the for errors before handling.
3. EAFP is enabled by exceptions. Without exceptions, error flow is interspersed in program flow
```py
from exceptional import convert
import sys
from math import log

DIGIT_MAP = {
    'eight': '8',
    'five': '5',
    'four': '4',
    'nice': '9',
    'one': '1',
    'seven': '7',
    'six': '6',
    'ten': '10',
    'three': '3',
    'two': '2',
    'zero': '0'
}

def convert(s):
    """Convert a string to an integer"""
    try:
        number = '' # Creates empty string
        for token in s:
            number += DIGIT_MAP[token] # Same as number = number + DIGIT_MAP[token]
        return int(number)
        
    except (KeyError, TypeError) as e: # e is the exception object.
        print(f'Conversion error: {e!r}', # ! after expression in f string object brings in information from the REPL.
        file=sys.stderr)
        pass # This is a no op. Allows us to have an empty block. Block can not be empty in Python.
    raise # Reraises the exception error on errors associated with string_log.

def string_log(s):
    v = convert(s)
    return log(v) # Compute natural log.
```
## Zero to Mastery Course
### Basics
##### Walrus :=
Assigns values to expressions. New in Python 3.8.
```py
x = "hellooooooooooo"
if (n := len(x)) > 10:
    print(f"The length of x is {n}")
```
### OOP 
1. Encapsulation, containing info in a class.
2. Abstraction, hides the details away, privacy or not _name.
3. Inheritance
4. Polymorphism
```py
class NameOfClass:
    class_attribute = 'value' 
    def __init__(self, param1, param2):
        self.param1 = param1 #attributes of the objects
        self.param2 = param2

    def method(self):
        #code
        #eg, print(f'my name is {self.name}')
        #return 'done' # If a function does not return anything it returns None
    
    @classmethod
    def cls_method(cls, param1, param2):
        #code
        #eg, return cls('Teddy', num1 + num2)
    
    @staticmethod
    def stc_method(param1, param2):
        #code
        #eg, return num1 + num2
```
##### Inheritance
The idea of a parent (User) and children classes (or sub-classes or derived classes) (Wizard, Archer, etc.). isinstance()
```py
#users can be wizards, archers, etc, but they must be signed in first.

class User():
    def sign_in(self): # No __init__ method because we dont need to assign attributes to the class.
        print('logged in')

class Book():
    def new_book(self):
        print(f'a class can inherit two classes using commas!')

class Wizard(User, Book):
    def __init__(self, name, power):
        self.name = name
        self.power = power
    
    def attack(self):
        print(f'attacking with a power of {self.power}')

class Archer(User):
    def __init__(self, name, num_arrows):
        self.name = name
        self.num_arrows = num_arrows
    
    def attack(self):
        print(f'attacking with arrows: arrows left- {self.num_arrows}')

wizard1 = Wizard('Merlin', 60)
print(isinstance(wizard1, Book))
wizard1.new_book()
```
##### Polymorphism
```py
#users can be wizards, archers, etc, but they must be signed in first.

class User():
    def sign_in(self): # No __init__ method because we dont need to assign attributes to the class.
        print('logged in')
    
    def attack(self):
        print('do nothing')

class Book():
    def new_book(self):
        print(f'a class can inherit two classes using commas!')

class Wizard(User, Book):
    def __init__(self, name, power):
        self.name = name
        self.power = power
    
    def attack(self):
        User.attack(self) # Polymorphism
        print(f'attacking with a power of {self.power}')

class Archer(User):
    def __init__(self, name, num_arrows):
        self.name = name
        self.num_arrows = num_arrows
    
    def attack(self):
        print(f'attacking with arrows: arrows left- {self.num_arrows}')

wizard1 = Wizard('Merlin', 60)
archer1 = Archer('Robin', 30)

def player_attack(char):
    char.attack() # Polymorphism. The object determines which attack method.

print(wizard1.attack())
```
#### super()
super() requires less code (see below where super() replaces User and thereby removes the need for self) and refers to the base class (User).
```py
super().__init__(param)
#User.__init__(self, param)
```
#### dir() allows introspection at runtime, ie., see what is available to an object.
```py
print(dir(wizard1))
```
#### dunder magic methods __magicmethods__
__str__ or str() are the same. You can customise or modify dunder methods if desired. Usually you wouldn't want to overwrite them but you can if you will.
```py
def __str__(self)
    return self.param # Now __str__ or str() will return that param instead of the default.
    
class Toy():
    def __init__(self, colour, age):
        self.colour = colour
        self.age = age
        self.my_dict = {
            'name':'Yoyo',
            'has_pets': False
        }

    def __call__(self): # __call__ allows you to call an object, action_figure in this case. 
        print('you called??')
    
    def __getitem__(self, i):
        return self.my_dict[i] # my_dict is a Toy class attribute.

action_figure = Toy('red', 0)

print(action_figure()) # Here we have called the object, which will print 'you called??'
print(action_figure['name']) # __getitem__ 
```
#### Extending List (essentially modifying the inbuilt classes).
How to return a new list class called a super list that always returns length 1000?
```py
class SuperList(list):
    def __len__(self):
        return 1000
```
#### Multiple Inheritance
```py
class HybridBorg(Wizard, Archer): Using two base classes!
    def __init__(self, name, power, num_arrows):
        Wizard.__init__(self, name, power) # This is how to access the attributes and methods in those classes.
        Archer.__init__(self, name, num_arrows) # This is how to access the attributes and methods in those classes.
``` 
#### Method Resolution Order (MRO)
What is first in line if calling multipe base classes?
```py
print(object.mro())
print(object.__mro__)
```

### Functional Programming
#### map, filter, zip, reduce
```py
from functools import reduce

#1 Capitalize all of the pet names and print the list
my_pets = ['sisi', 'bibi', 'titi', 'carla']

def capitalise(string):
  return string.upper()

print(list(map(capitalise, my_pets)))

#2 Zip the 2 lists into a list of tuples, but sort the numbers from lowest to highest.
my_strings = ['a', 'b', 'c', 'd', 'e']
my_numbers = [5,4,3,2,1]

print(list(zip(sorted(my_numbers), my_strings)))

#3 Filter the scores that pass over 50%
scores = [73, 20, 65, 19, 76, 100, 88]

def passgrade(item):
  return item > 49 

print(list(filter(passgrade, scores)))

#4 Combine all of the numbers that are in a list on this file using reduce (my_numbers and scores). What is the total?

def accumulater(acc, item):
  return acc + item

print(reduce(accumulater, (my_numbers + list(filter(passgrade, scores)))))
```
#### map() preforms a function of an iterable
Map could for example be used to change all the names in a list to capital letters quickly.
```py
my_list = [1,2,3]
def multipybytwo(item):
    return item*2
print(list(map(multipybytwo, my_list))) # Pure funciton because it does not afffect the outside world, ie., my_list is not altered, rather a new list was made.
```
#### filter() essentially filter the results that map would return
```py
def checkodd(item):
    return item % 2 != 0

print(list(filter(checkodd, my_list)))
```
#### zip() puts iterables together
```py
my_list = [1,2,3]
your_list = [10,20,30]
print(list(zip(my_list, your_list))) # Could be any combination of iterables.
```
#### reduce
```py
from functools import reduce
def accumulator(acc, item):
    print(acc, item)
    return acc + item

print(reduce(accumulator, my_list, 0)) # Initial value set to zero (acc in accumulator definition).
```
#### lambda (annonymous one off function, lambda param: action(param)
Called anonymous functions in some languages.
```py
double = lambda x: x*2
print(double(1)) # Returns 2

my_list = [1,2,3]
print(list(map(lambda item: item*2, my_list)))

print(reduce(lambda acc, item: acc+item, my_list, 10)) # Returns 16.

# A common way to adjust sorting on iterables.
a = [(0,2), (4,3), (9,9), (10, -1)]
a.sort(key=lambda x: x[1]) # x is the tuple and the key will be in the second item.
print(a)
```
#### list comprehensions (or set or data comprehensions)
Quick ways to generate sets, etc. 
my_list = [param for param in iterable]
```py
my_list = [param for param in iterable]
my_list = [char for char in 'hello']

my_list2 = [num for num in range(0, 100)]
my_list2 = [num for num in filter(lambda item: item % 2 !=0, range(0, 100))] # This is too much coding compared with the example below.
my_list6 = [num for num in range(0, 100) if num % 2 == 0] # Which returns the same as my_list2 above.
my_list3 = [num for num in filter(lambda item: item not in my_list, range(0, 100))]
my_list4 = [num*2 for num in range(0, 100)]
```
#### list and dictionary comprehensions
Sets are the same as lists, just use {}.
```py
simple_dict = {
    'a': 1,
    'b': 2
}
my_dict = {k:v**2 for k, v in simple_dict.items() if v%2 ==0}
print(my_dict)

my_dict1 = {num:num*2 for num in [1,2,3]} # Returns {1: 2, 2: 4, 3: 6}

some_list = ['a', 'b', 'b', 'h', 'f', 'n', 'n']
duplicates = list(set([x for x in some_list if some_list.count(x) > 1]))
print(duplicates)
```
### Decorators (known as a decorator pattern).
1. Decorators give extra functionality to functions.
2. A hirger order function (HOR) accepts another function as a parameter or returns another function.(ie, map(), reduce(), filter()!
```py
def my_decorator(func):
    def wrap_func(*args, **kwargs): # *args means all arguments (parametres) and **kwargs means all keyword arguments.
        print('********')
        func(*args, **kwargs)
        print('********')
    return wrap_func

@my_decorator
def hello(greeting, emoji = ':)'):
    print(greeting, emoji)

hello('hiiii')
```
Decorators can help with measuring performance!:
```py
from time import time

def performance(fn):
    def wrapper(*args, **kwargs):
        t1 = time()
        result = fn(*args, **kwargs)
        t2 = time()
        print(f'took {t2-t1} s')
        return result
    return wrapper


@performance
def long_time():
    for i in range(1000000):
        i * 5

long_time()
```
Or for authentication:
```py
# Create an @authenticated decorator that only allows the function to run is user1 has 'valid' set to True:
user1 = {
    'name': 'Sorna',
    'valid': True
}

def authenticated(fn):
  def wrapper(*args, **kwargs):
    if args[0]['valid']:
        return fn(*args, **kwargs)
  return wrapper

@authenticated
def message_friends(user):
    print('message has been sent')

message_friends(user1)
```
### Error Handling (Exceptions)
try and except blocks are used to handle exceptions
```py
while True:
    try:
        age = int(input('what is your age?'))
        10/age

    except ValueError:
        print('please enter a number')
        continue
    except ZeroDivisionError:
        print('please enter an age above zero')
    else:
        print('thanks')
        break
    finally: # Finally will run at the end of each loop no matter what, exception or no exception.
        print('ok I am finally done')
    print('this will never print because we have break under else')
```
Combining exceptions:
```py
def sum(num1, num2):
    try:
        return num1 / num2
    except (TypeError, ZeroDivisionError) as err:
        #print(f'please enter numbers: error as follows - {err}')
        print(err)
```
Raising an exception is also possible:
```py
while True:
    try:
        age = int(input('what is your age?'))
        if age < 18:
            raise Exception('must be above 18')
    #except etc etc code.
```
### Generators
1. Generate a sequence of values over time. 
2. Range() is a generator. 
3. Generators are not stored in memory, rather they give you one item at a time to work with.
4. Generators are iterables, ie. you can loop over them. But iterables like list etc. are not generators.
5. Use less resources because they are MUCH faster than iterating over an iterable like a list.
```py
def generator_function(num):
    for i in range(num):
        yield i * 2 # Yield will return the number one at a time and this can be used with next().
        
g = generator_function(100)
print(next(g)) # Would return 0 (0*2). If you exceed the next yield you recieve a stop iteration error.
```
Performance of generators:
```py
@performance
def long_time():
    print('1')
    for i in range(1000000): 
        i*5

@performance
def long_time2():
    print('2')
    for i in list(range(1000000)):
        i*5
```
Under the hood of a for loop: iter()
```py
# The below is essentially under the hood in a for loop.
def special_forloop(iterable):
    iterator = iter(iterable) # Note the iter() method, which turns each number into an iterable object.
    while True:
        try:
            print(iterator)
            print(next(iterator)*2)
        except StopIteration:
            break

special_forloop([1,2,3])
```
Under the hood of range:
```py
#The class MyGen mimics what range does under the hood.
class MyGen():
    current = 0
    def __init__(self, first, last):
        self.first = first
        self.last = last

    def __iter__(self): # __iter__ built into python
        return self

    def __next__(self): # __next__ built into python
        if MyGen.current < self.last:
            num = MyGen.current
            MyGen.current +=1
            return num
        raise StopIteration

gen = MyGen(0, 100)
for i in gen:
    print(i)
```
Fibonacci Numbers
```py
def fib(number):
    a = 0
    b = 1
    for i in range(number):
        yield a 
        temp = a
        a = b
        b = b + temp

for x in fib(1000):
    print(x)
```
### Modules
1.__pycache__ is created when we import modules and speeds things up. We dont touch this.
2. A .py file is a module, but a package is a level up, its a folder.
3. if __name__ == __main__: means, if this is the main file, run it (as opposed to modules that are just to be imported).
4. Python has a built in package index!
5. import sys, sys.argv[1] etc allows you to provide arguments from the terminal.
6. Virtual environments allow projects to have versioned libraries, which is important due to dependencies. 
7. Specialised data types are built into python. Eg. From collections import Counter. or datetime or array.
8. Arrays use less memory than lists. 
```py
from random import shuffle
my_cards = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
random.shuffle(my_cards)
print(my_cards[0:6])

import sys
first = sys.argv[1]
last = sys.argv[2]
print(f'hiiii! {first}{last}')
# In the terminal you would enter: python module.py arg1 arg2

from collections import Counter, defaultdict, OrderedDict
# defaultdict is a default dict from Python 3.6.

#li = [num for num in range(1, 8)]
li = [1, 2, 3, 4, 5, 6, 7, 7]
sentence = 'blah blah blah thinking about python'
print(Counter(li)) # Retruns a dict where value is the count of list contents.
print(Counter(sentence))

dict = defaultdict(lambda: 'key does not exist', {'a': 1, 'b': 2}) # if int was used it would return 0, as int alone = 0
print(dict['c']) # Returns 'key does not exist' instead of key error.

d = OrderedDict()
d['a'] = 1
d['b'] = 2

d2 = OrderedDict()
d2['a'] = 2
d2['b'] = 1

print(d2==d) # Returns False, but normal dictionaries would be True in Python older than 3.6!
print(d2 is d) # Returns False of course. 

import datetime

print(datetime.time(5,45,2))
print(datetime.date.today())

from array import array

arr = array('i', [1,2,3]) # i stands for signed integer. https://docs.python.org/3/library/array.html#module-array
print(arr[0]) # This uses much less memory!
```
### How to debug code
pdb The python debugger. How to debug?
1. linting, pylint etc, highlighting on text to show mistakes.
2. use IDEs like pycharm
3. learn to read errors
4. pdb, the python debugger.
```py
import pdb

def add(num1, num2):
    pdb.set_trace() # Common arguments are step, arg, list, help, help list etc. You can change variable values etc in the pdb to assist with debugging!
    t = 4*5
    return num1 + num2

add(4, 'SDfasg')
```
### Files I/O, input and output
1. r+ means read and write, r to read, a is append, w is write. w will write over.
2. write will create a new file if it does not exist.
3. ./ at the beginning of the file path means current folder.
4. ../ at the beginning means go back one directory.
```py
my_file = open(r'test.txt')

# seek is used to return the curser to the start of the file, otherwise the next two print statements would return blank.
my_file.seek(0)  # 0 is the first curser index in the file
print(my_file.read())
my_file.seek(6)
print(my_file.read())
my_file.seek(0)


print(my_file.readline()) # returns one line
print(my_file.readlines()) # returns all lines

my_file.close() # you must close the file!

with open('sad.txt', mode='w') as my_file:
    text = my_file.write(':(')
    print(text)
```
#### File Paths
```py
from pathlib import Path
ykr_grid_file_path = Path("MetropAccess_YKR_grid\MetropAccess_YKR_grid_EurefFIN.shp")
```
#### Files I/O errors, using try and except.
```py
try:
    with open('sad.txt', mode='w') as my_file:
        print('write something and press enter twice')
        text = my_file.write(input())
        print(f'{text} characters were added to {my_file}')
except FileNotFoundError as err:
    print('file does not exist')
    raise err
except IOError as err:
    print('IO error')
    raise err
```
### Regular Expressions
1. Search python regex for websites with sets and keys for building patterns.
2. use this to build: https://regex101.com
3. Regex is great for validation!
```py
#email validation
import re

pattern = re.compile(r"(^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$)") #email validation copied from google and checked here: https://regex101.com/

string = 'b@b.com'

#print('search' in string)

a = pattern.search(string)
b = pattern.findall(string)
c = pattern.fullmatch(string) # true if completely identical
d = pattern.match(string)

print(a.span()) # shows where in string the search occurs
print(a.start()) # shows where it starts 
print(a.group()) # returns matches
print(a.group(1)) # only prints results from group one (([a-zA-Z]))

#password validation 
import re

pattern = re.compile(r"[a-zA-Z0-9#%$@]{8,}\d")

password = 'gegwedss$#%5'

a = pattern.fullmatch(password)

print(a)

# conditions were min 8 charactors
# can contain #%$@
# must end with a number
```
Snippets:
```
PATTERN = \bcluster.*\b
```
### Git Hub command line commands
1. git clone pastelinktorepohere
2. git status, git add *, git commit -m "message", git push
3. git pull
4. git branch # see branch directory
5. git branch littlefeature # create a branch called littlefeature
6. git checkout littlefeature # switches to branch littlefeature

7. git push origin <your_branch_name> --force

#### To connect repo to exisiting directory, git 2.27
7. git init, then, git checkout -b main
8. git add *
9. git commit -m "First commit"
10. git remote add origin remote repository URL
11. git remote -v
12. git push origin main

#### Git ignore
1. Before first commit: Make .gitignore in notepad, 1) Open Notepad, 2) Add the contents of your gitignore file. 3) Click "Save as" and select "all files".4) Save as .gitignore.
2. After first commit the particular files or folders will need to be untracked using git rm --cached FILENAME
3. use this link for more details: https://www.pluralsight.com/guides/how-to-use-gitignore-file

#### Next , git remote add, git push origin master.


## Web Development in Python using Flask
1. Flask is a microframework. Django is a framework, a big kitchen to enter where you can start cooking up your website.

2. python -m venv venv # create a virtual env in the project directory.
3. venv\Scripts\activate # activate the env.
4. C:\path\to\app>set FLASK_APP=server.py.
5. Development mode SET FLASK_DEBUG=1, then python -m flask run. If not development mode then just python -m flask run.

6.C:\Users\Shane Rich\webserver>pip freeze > requirements.txt # creates a list of requirements for this app to be run on other machines! This is why we use environments!

### Testing, Unit Testing
1. Every main.py file should have its own test.py file.
2. Test.py is only for development, not for production ie., customers never see this.
3. Standard library is called unittest.
4. Break the function in the test, trick it into causing an error, then improve the function  by catching it and asserting it. 
5. REPL> python -m unittest (will run all test files due to unittest.main() at bottom of test files). Not necessary to use python test.py unless wanting to run an individual test.py file.
6. python -m unittest -v (v stands for verbose).
7. Remember to review my tutorial test.py file in the python_tutorial repo.
8. doc string like comments can be added to tests for use with python -m unittest -v
9. setUp() is a default method in unittest that will run before every test. use it to set up variables for example.
10. tearDown() is another default method executed after every test. Often used when interacting with databases.

### Higher Order Functions
```
# Instead of creating many increment function one can write a higher order function hof_add
def hof_add(increment): 
    # Create a function that loops and adds the increment
    def add_increment(numbers):
        new_numbers = []
        for n in numbers:
            new_numbers.append(n + increment)
        return new_numbers
    # We return the function as we do any other value
    return add_increment

add5 = hof_add(5)
print(add5([23, 88]))   # [28, 93]
add10 = hof_add(10)
print(add10([23, 88]))  # [33, 98]
```
#### Map and Filter are examples of built in higher order functions
Map
```
names = ['Shivani', 'Jason', 'Yusef', 'Sakura']
greeted_names = map(lambda x: 'Hi ' + x, names)

# This prints something similar to: <map object at 0x10ed93cc0>
print(greeted_names)
# Recall, that map returns an iterator 

# We can print all names in a for loop
for name in greeted_names:
    print(name)
```
Filter returns only values that evaluate to True
```
numbers = [13, 4, 18, 35]
div_by_5 = filter(lambda num: num % 5 == 0, numbers)

# We can convert the iterator into a list
print(list(div_by_5)) # [35]
```

### Maching Learning and Data Science
#### Cleaning Data
```py
var = df['column'].replace('[\$,]', '', regex=True).apply(value_to_float) # regex101.com

def value_to_float(x):
    if type(x) == float or type(x) == int:
        return x
    if 'K' in x:
        if len(x) > 1:
            return float(x.replace('K', '')) * 1000
        return 1000.0
    if 'M' in x:
        if len(x) > 1:
            return float(x.replace('M', '')) * 1000000
        return 1000000.0
    if 'B' in x:
        return float(x.replace('B', '')) * 1000000000
    return 0.0

    df."Insert data series column" = df."Insert data series column" .apply(value_to_float)
```
## Pandas and Geopandas
### Functions
```py
df.apply() #Functions
```
## File and Paths
```py
from pathlib import Path

data_folder = Path("source_data/text_files/")

file_to_open = data_folder / "raw_data.txt" # If you want to add on to the path, you can use the / operator directly in your code.

print(file_to_open.read_text())


if not filename.exists():
    print("Oops, file doesn't exist!")
else:
    print("Yay, the file exists!")
```
To make paths compatible in all operating systems (windows uses the opposite slash to everythin else) use:
```py
from pathlib import Path

filename = Path("source_data/text_files/raw_data.txt")
```
Here’s an example that will open a local file in your web browser with just two lines a code:
```py
from pathlib import Path
import webbrowser

filename = Path("source_data/text_files/raw_data.txt")

webbrowser.open(filename.absolute().as_uri())
```
```py
from pathlib import Path

file_name = Path(file_path).name  # myfile.png
file_stem = Path(file_path).stem  # myfile 
```
