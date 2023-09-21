# References
[back to index](./INDEX.md)
## General
- **reference** is an **alias** to already-existing object or function
  - it is usually implemented as a pointer by compiler, but it can be optimized out
- there are two types of references:
  - `T& ref` - **lvalue reference** to type `T`
  - `T&& ref` - **rvalue reference** to type `T` *(since C++11)*
- **references** are not **objects**:
  -  do not necessarily occupy **storage**
  -  there are not **references** to **references**
  -  there are no **arrays**, nor **pointers** to **references**
- **references** cannot be *cv-qualified* at the top level
-  they are no **references** to **void**
-  **const lvalue reference** and **rvalue references** extend the lifetime of temporary object, when bound to it
   -  **rvalue references** used for that purpose have the advantage of being able to modify referenced object
   -  (both of them can be bound to **xvalue**)
- when the lifetime of object referenced outlives the lifetime of reference, the referense is *dangling*
  - accessing dangling reference is **undefined behavior**
- when a **function** has both rvalue reference and lvalue reference **overloads**:
  - the rvalue reference overload binds to rvalues
    - **prvalue** -> rvalue reference
    - **xvalue** -> rvalue reference
  - the lvalue reference overload binds to lvalues:
    - **lvalue** -> lvalue reference
  - this behavior is crucial part of **move semantic** and enables **move constructors**, **move assignments** and another *move-aware* functions to be called due to those **overload resolution** rules


## Lvalue references
- can be used to **alias** an existing object (optionally with different cv-qualification)
- allow *passing by reference* to function
- if function return type is **lvalue reference**, the function call expression becomes an **lvalue expression** (being assignable: `fun() = 5`)

## Rvalue references
- can be bound to **rvalues** (*xvalues* and *prvalues*) 

## Reference collapsing
- due to type manipulations in **templates** or **typedefs**, references to references may be formed and in such case the **collapse**
-  rvalue reference to rvalue reference collapses to rvalue reference, all other combinations form lvalue reference:
   -  `T&& &&` -> `T&&`
   -  `T& &&` -> `T&`
   -  `T&& &` -> `T&`
   -  `T& &` -> `T&`
-  this behaviour is crucial for **perfect forwarding**


## Forwarding references
- special kind of references that **preserve the value category** of a function argument, making it possible to *forward* further along with **value category** using `std::forward`
### There are two ways to create forwarding reference:
- function parameter of a function template declared as **rvalue reference** to cv-unqualified type template parameter of that same function template:

        template<class T> int f(T&& x) {      // x is a forwarding reference
            return g(std::forward<T>(x)); // and so can be forwarded
        }

- `auto&&` except when deduced from a brace-enclosed initializer list:
  
        auto&& obj = fun1(); //obj is a forwarding reference
        fun2(std::forward<decltype(obj)>(obj)); //so it can be forwarded
    
    - `auto&& z = {1, 2};` is not a forwarding reference
    - this is handy to use in *range for* loops: `for (auto&& x: f()) {...}` to ensure that we are **moving** whenever we can