---
title: "Error: Expected ';'"
---
- A statement in C3 ends with a semicolon `;`
- Below: a simple function call statement, the line ends with `;`
```
some_function_call();
```
- Note that Structs and Unions are not terminated with `;`.
- Below is invalid and will throw: `Error: ';' wasn't expected here, try removing it.`
```
struct MyStruct{
    int a;
};
```
