---
title: "WASM @extern"
---
- @wasm
- @extern("NAME")
- A function that is to be called from JavaScript should be marked with @wasm and @extern
- From JavaScript these functions are exposed as: wasm.instance.exports.NAME
```
fn void onclick( int x, int y ) @extern("onclick") @wasm {
	js_eval(`
		window.alert("hello click")
	`);
}
```
- Above, the function is exported to JavaScript and callable as: `wasm.instance.exports.onclick(x,y)`
