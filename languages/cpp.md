# Cpp

[Inheritance](https://www.tutorialspoint.com/cplusplus/cpp_inheritance.htm)

## Pointer

* `*(adr)` deref_func = return val inside adr
* `&(val)` ref_func = return adr pointer of the val
* `&(*(adr))` = get back adr

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

* foo is public
* _bar is protected
* __baz is private
