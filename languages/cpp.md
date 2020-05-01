# Cpp

[Inheritance](https://www.tutorialspoint.com/cplusplus/cpp_inheritance.htm)

## Debug

Using `gdb` http://users.ece.utexas.edu/~adnan/gdb-refcard.pdf

- `b` - Puts a breakpoint at the current line
- `d N` - Deletes breakpoint number N
- `info break` - list breakpoints
- `c` - Continues running the program until the next breakpoint or error
- `r` - Runs the program until a breakpoint or error
- `f` - Runs until the current function is finished
- `s` - Runs the next line of the program
- `n` - Like s, but it does not step into functions
- `p var` - Prints the current value of the variable "var"
- `bt` - Prints a stack trace
- `u` - Goes up a level in the stack
- `d` - Goes down a level in the stack
- `q` - Quits gdb

## Pointer

- `*(adr)` deref_func = return val inside adr
- `&(val)` ref_func = return adr pointer of the val
- `&(*(adr))` = get back adr

```cpp
int x = 1111;
int* adr = &x; // 0x010fffff
int& deadr = *adr; //1111


&&x //err
**x //err

&*adr // 0x010fffff
&*deadr //err

*&adr // 0x010fffff
*&deadr  //1111
```

## Naming Conv

- foo is public
- \_bar is protected
- \_\_baz is private
