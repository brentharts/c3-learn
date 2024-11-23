---
title: "WASM JavaScript Bridge"
---
- WASM is loaded by JavaScript using: `WebAssembly.instantiate`.
- The first argument to `WebAssembly.instantiate` is the wasm file (ArrayBuffer of bytes)
- The second argument to `WebAssembly.instantiate` is an Object with `env`. 
```
extern fn int   js_eval(char*ptr);

fn void onclick( int x, int y ) @extern("onclick") @wasm {
	js_eval(`
		window.alert("hello click")
	`);
}
```
- The above C3 code calls `js_eval` passing a string to eval in JavaScript.
- Below is an example JavaScript bridge (`env`).
```
class myapi{
	reset(wasm){
		this.wasm=wasm;
	}
	get_env(){
		return make_environment(this)
	}
	js_eval(a){
		return eval(cstr_by_ptr(this.wasm.instance.exports.memory.buffer,a))
	}
	onclick(e){
		console.log("onclick:", e);
		this.wasm.instance.exports.onclick(e.x,e.y)
	}
}
```
- Above requires these JavaScript helper functions
```
function make_environment(e){
	return new Proxy(e,{
		get(t,p,r) {
			if(e[p]!==undefined){return e[p].bind(e)}
			return(...args)=>{throw p}
		}
	});
}

function cstrlen(m,p){
	var l=0;
	while(m[p]!=0){l++;p++}
	return l;
}

function cstr_by_ptr(m,p){
	const l=cstrlen(new Uint8Array(m),p);
	const b=new Uint8Array(m,p,l);
	return new TextDecoder().decode(b)
}
```
