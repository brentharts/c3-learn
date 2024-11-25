---
title: "Error: Expected the ending ')' here."
---
- A function call in C3 begins with the function name,
- followed by the function arguments in parenthesis.
- FUNCTION_NAME( OPTIONAL_ARGUMENTS,... )
```
some_function_call( a, b, c);
```
- Below, is missing the closing parenthesis, and throws: `Error: Expected an ending ')'. Did you forget a ')' before this ';'?`
```
some_function_call(a,b,c;
```

