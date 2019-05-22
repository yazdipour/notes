# Python

* http://pythonfiddle.com/
* https://github.com/Junnplus/awesome-python-books
* https://radimrehurek.com/gensim/
* https://www.pythonsheets.com/
* https://godjango.com/
* [An A-Z of useful Python tricks](https://medium.freecodecamp.org/an-a-z-of-useful-python-tricks-b467524ee747)
* [Writing Comments in Python](https://realpython.com/python-comments-guide/)
* [Look Ma, No For-Loops: Array Programming With NumPy](https://realpython.com/numpy-array-programming/#.W9dFkY85HMs.twitter)

## Basics

```py
from DIRECTORY import ClassName
#| DIRECTORY >
#		| fileName.py {class ClassName}
#		| __init__.py {from fileName import ClassName}
del obj
raw_input() # Don’t use input(), eval, exec cause of security problems
** # Math.Pow
Var=8 if(1==1) else 9 # ?:
import sys; sys.argv # Get Input from CLI

# String - immutable
# ' for words | " for sentence | """ for multiline in CLI
print("\a") #beep
formattedStr = "%s - %d", ('Ali',33)
rawStr = r'hello\t' #gonna be hello\t
mStr.find('x') # indexOf
'-'.join(1,2,3) # 1-2-3
mStr.strip() # trim
mStr.strip("-") # trim - from start & end
mStr.lstrip() # left trim
mStr.rstrip() # right trim
mStr[2]= 'a' # ERROR - immutable

# Raise Exception
raise <ExpType>, 'msg' # one way
assert(condition) # or if assert(false) then will raises exception
# Try Catch
try:
	foo
except IOError, e:
	bar
else:
	# if no exception appeared
finally:
	# run this no matter what
# ARRAY
arr.remove(obj)
del arr[1:3] #[1,2,3,4,5] >> [1,5]
list(mTuple) # tuple to list
h_letters = [ letter for letter in 'human' ] #['h', 'u', 'm', 'a', 'n']
cmp(list1,list2) # compare
l.reverse(); l.sort()
x = [1, 2, 3]; x.append([4, 5]) # [1, 2, 3, [4, 5]]
x = [1, 2, 3]; x.extend([4, 5]) # [1, 2, 3, 4, 5]
l.pop(obj) # return and remove
b = a # copy by reference
b = a[:] # copy by value

# TUPLE - immutable
tuple(mList) # list to tuple
def foo(*items): # like foo(int.. items) in JAVA
	for i in items:
		print(i)
# DICTIONARY
zipped = zip(keysArr, valueArr) # [1,2],[3,4] > [(1,3), (2,4)]
(keysArr, valueArr) = *zipped # unzipping
d.items()
d.has_key(k); d.fromkeys(ks)
def f(**dic):
	for i in dic:
		print(i,dic[i]2)
```

## Lambda

`lambda p1, p2: p1*p2`

## Functions

```py
# Comment
def foo():
	'func commenting'
	bar()

# CallByObject
def foo(v):
	v += 1 # when u still the obj ref, you play with it and the original object will change
	v = 30 # but when you re-assign it, you will get disconnected from the original object. Now v, is like a local variable
	print(v) #30
v = 2
foo(v)
print(v) #3

# Scope
b=4
def foo():
	global b
	print(b)
```

## * & **

```python
>>> def z(x):print(x);
...
>>> d = {'x':1}
>>> z(*d) //Arg
x
>>> z(**d)  //keyArg
1
```

```python
def foo(x,y):
    print('%s %s' % (x,y))

>>foo(*(1,2))
>>foo(*[1,2])

bar= (x* x for x in range(2))
>> foo(*bar) # 1 2

dic= {'a':1,'y':2}
>> foo(**dic) ## 1 2
```

```python
def foo(a,*b,**c): # only 'a' is required
	print(a)
	print(b)
	print(c)

>>>foo('hello',1,2,3,key1=1,keyX='3')
hello
(1,2,3)
{'key1':1 , 'keyX':'3'}
```

## Merging Dictionaries

```python
x={'a':1,'c':9}
y={'b':2,'a':3}
z={**x,**y} # {'a':3,'b':2,'c':9} -- right ones have higher priorities
```

## Type

```python
def x(a:int) -> int:
    return a + 1

# mypy xx.py
```

## is vs ==

"is" statement is a syntactic sugar for "id(a) == id(b)"

```python
a = [1,2,3]
b = a
c = [1,2,3] # or c = list(a) -> will clone

print(a==c) #True
print(a is c) #False
print(a==b) #True
print(a is b) #True
print(b==c) #True
print(b is c) #False
```

> ### برابری Equality
> توی پایتون وقتی می‌خواهیم ببینم دو آبجکت با هم برابر هستند یا خیر، از عملگرهای == و =! استفاده می‌کنیم.
> ### هویت Identity
> در مقابل‌ این عملگرها، دوتا عملگر دیگه هم داریم که is و is not هستند. is بررسی می‌کنه که آیا این آبجکت دقیقا یک آبجکت هستند یا نه. دقت کنید،  یعنی اون دو متغییر دقیقاً در یک مکان از حافظه قرار گرفتند 

## _, __

```python
class X:
	def __init__(self):
		self.foo = 1
		self._bar = 2
		self.__baz = 3
dir(X())
>>> [
	'_X__baz',	# private (to access private var, add _CLASS at first of the variable name)
	'_bar',		# public
	'foo'		# public
]
```

## return None, Implicit return

return None == return

```python
def foo():
	if(True): return 1
	else: return None
# SAME AS
def foo():
	if(True): return 1
```

## Switch alternative

```python
def foo(op,x,y):
	return {
		'add': lambda: x+y,
		'sub': lambda: x-y
	}.get(op,lambda: None)()
```

## Class

```py
class x (parentY, parentZ):
	'class doc'
	x.__doc__ #to see class doc
	def __init__(self): # constructor
	def __del__(self): # deconstructor
	issubclass(x,parentY) # bool
	isinstance(obj,x) # bool
	getattr();setattr();hasattr();delattr()
	self.__class__.__name__ #Get Class name in string
```

## SimpleHTTPServer

```py
python -m SimpleHTTPServer 8000

import SimpleHTTPServer
import SocketServer
PORT = 8000
Handler = SimpleHTTPServer.SimpleHTTPRequestHandler
httpd = SocketServer.TCPServer(("", PORT), Handler)
print "serving at port", PORT
httpd.serve_forever()
```