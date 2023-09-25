# WebAssembly (Wasm)
[back to main index](../README.md)

## General
* **Wasm** is direct succesor of **asm.js**
* **Emscripten** used to be **asm.js** compiler
* before compilation the module is **validated** in a single pass
* **module** is fully compiled to machine code before running - **ahead of time(AOT) compilation**
* it uses the same VM that JS for execution
* **Emscripten** is a **backend** to **LLVM**, uses **Clang** as a **frontend**
* **Wasm** supports 4 data types:
  * `i32` : 32-bit integer
  * `i64` : 64-bit integer
  * `f32` : 32-bit float
  * `f64` : 64-bit float

## Memory
* **heap** is stored seperately from **stack**
* **heap** is passed from host as a `ArrayBuffer`
* runtime verifies that accesses are withing the bounds