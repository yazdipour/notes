# Python

## * **

```python
def x(x,y):
    print('%s %s' % (x,y))

x(*(1,2))
x(*[1,2])
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