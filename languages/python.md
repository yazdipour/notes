# Python

* http://pythonfiddle.com/
* https://github.com/Junnplus/awesome-python-books
* https://radimrehurek.com/gensim/
* https://www.pythonsheets.com/

## Tutorial

* https://godjango.com/
* [An A-Z of useful Python tricks](https://medium.freecodecamp.org/an-a-z-of-useful-python-tricks-b467524ee747)
* [Writing Comments in Python](https://realpython.com/python-comments-guide/)
* [Look Ma, No For-Loops: Array Programming With NumPy](https://realpython.com/numpy-array-programming/#.W9dFkY85HMs.twitter)

## Server

`python -m SimpleHTTPServer 8000`

## * **

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

> برابری Equality

> توی پایتون وقتی می‌خواهیم ببینم دو آبجکت با هم برابر هستند یا خیر، از عملگرهای == و =! استفاده می‌کنیم.

> هویت Identity

> در مقابل‌ این عملگرها، دوتا عملگر دیگه هم داریم که is و is not هستند. is بررسی می‌کنه که آیا این آبجکت دقیقا یک آبجکت هستند یا نه. دقت کنید،  یعنی اون دو متغییر دقیقاً در یک مکان از حافظه قرار گرفتند 

## _, __

```python
class X:
	def __init__(self):
		self.foo = 1
		self._bar = 2
		self.__baz = 3
dir(X())
>>> ['_X__baz', # private!
'_bar',			# public!
'foo'			# public!
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