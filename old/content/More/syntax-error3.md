---
title: "Error: A type name was expected"
---
- C3 functions are defined as: `fn RETURN_TYPE NAME ( ARGS...)`,
- Just like in C the return type of the function comes before the function name.
```
fn void myfunc() {}
```
- Below, is invalid, the return type is missing:
```
fn myfunc() {}
```
- Above will throw this error: `Error: A type name was expected, but this looks a variable or function name (as it doesn't start with an uppercase letter).`
