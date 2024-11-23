---
title: "WASM external functions"
---
- External functions are provided by the runtime environment or the linker.
- When C3 compiles for the WASM target the runtime environment is a JavaScript object.
- In the example below `js_eval` is declared as an external function that is provided by the JavaScript object. 
```
extern fn int   js_eval(char*ptr);

fn void onclick( int x, int y ) @extern("onclick") @wasm {
	js_eval(`
		window.alert("hello click")
	`);
}
```
- In JavaScript `js_eval` is defined as:
```
	js_eval(a){
		return eval(cstr_by_ptr(this.wasm.instance.exports.memory.buffer,a))
	}

```
