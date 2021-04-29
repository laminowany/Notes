# Functions
[back to index](../README.md)

## General
- function arguments are evaluated in undefined order
- local objects are destroyed in order reversed to construction
- inline before function return type is only a suggestion, not enforcement
  

## Return Type Deduction (since C++14)
If the **decl-specifier-seq** of the function declaration contains the keyword **auto**, **trailing return type** may be omitted, and the return type   will be deduced from the type of the expression used in the return statement.
- if the return type does not use **decltype(auto)**, the deduction follows the rules of **template argument deduction**
- if the return type is **decltype(auto)**, the return type is as what would be obtained if the expression used in the return statement were wrapped in **decltype**
- if there are multiple return statements, they must all deduce to the same type
- **virtual functions** and **coroutines** cannot use **return type deduction**
- if the return statement uses a **brace-init-list**, deduction is not allowed

## Abbreviated function template
If placeholder type (**auto**/**Concept auto**) appears in **function** or **function template** parameter list, then declaration declares a **function template**, and one **invented template parameter** for each placeholder is appended to the **template parameter list**.