# WebAssembly (Wasm)
[back to main index](../README.md)

## Benefits
- transfering Wasm module is fast due to compact binary format
- can be easily validated and compiled while streaming
- language evolution indepented from JavaScript!

## [Emscripten](./Emscripten.md)

## General
- **Wasm** is direct succesor of **asm.js**
- **Emscripten** used to be **asm.js** compiler
- before compiation the module is **validated** in a single pass
- **module** is fully compiled to machine code before running - **ahead of time(AOT) compilation**
- name **module** can refer both to:
  - binary file
  - compiled file
- it uses the same VM that JS for execution
- **Wasm** supports 4 data types:
  - `i32` : 32-bit integer
  - `i64` : 64-bit integer
  - `f32` : 32-bit float
  - `f64` : 64-bit float
- cannot access **DOM** or **WebAPI** directly

## Memory
- **heap** is linear memory stored seperately from **stack**
- **heap** is passed from host as a `ArrayBuffer`
- **stack** is not accessible by the code
- runtime verifies that accesses are withing the bounds

## [Module structure](./ModuleStructure.md)

## Runtimes
- thanks to WebAssembly Standard Interface (WASI), Wasm can be run outside of browsers (i.e. Node)
- **WebAssembly JavaScript API** is used to load and instantiate Wasm modules
  - `WebAssembly.instantiateStreaming(wasm, [importObject])` returns `{module: {...}, instance: {...} }`
    - `importObject` contains imported symbols and **Memory**
      - i.e. 
      ```js
      const importObject = {
        env: { 
          memory: new WebAssembly.Memory({initial: 1, maximum: 10})    
        } 
      };
      ```
      -  `importObject` must contain everything that is imported by Wasm module (i.e. `__memory_base`, `__table_base`)
    - `module` can be instantiated again or passed
    - `instance` contains exported functions from Wasm
  - `compileStreaming()` is similiar but only returns compiled module