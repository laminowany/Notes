# Optimization and Performance
[back to index](../README.md)

## General
- compilers are free to optimize the code by doing whatever they want, as long as the *observable side effects* are not changed, with two exceptions:
  - **copy ellision**
  - **allocation elision and extension** (since C++14)