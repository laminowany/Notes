# Classes
[back to index](../README.md)

## General
- **classes** and **structs** are basically the same in C++, the only difference is the default access modifier:
  - **public** for structs
  - **private** for classes

## Static data members
- **static** data members can be declared **inline** and initialized in the class definition since C++17

## Non-static member functions
### Ref-qualified member functions
A non-static member function can be declared with:
- no ref-qualifier - `void f() {...}`
  - implicit object parameter has type **lvalue reference** to cv-qualified X and is additionally allowed to bind **rvalue** implied object argument
- lvalue ref-qualifier - `void f() & {...}`
  - the implicit object parameter has type **lvalue reference** to cv-qualified X
- the rvalue ref-qualifier - `void f() && {...}`
  - the implicit object parameter has type **rvalue reference** to cv-qualified X
  
**No ref-qualifed overload** cannot be mixed with **ref-qualified overloads**.

Unlike **cv-qualification**, **ref-qualification** does not change the properties of the `this` pointer: within a **rvalue ref-qualified** function, `*this` remains an **lvalue expression**.


## Nested classes
Class declared inside other class is **nested class**:
- the name of the **nested class** exists only in the scope of the **enclosing class**
- **nested class** can use any members of the enclosing class
  -  it has access to all names to which enclosing class has access (*private, protected, ...*)
  -  it has no special access to  **this** pointer of the enclosing class
- name lookup from a member function of a **nested class** visits the scope of the **enclosing class** after examining the scope of the **nested class**
- **friend functions** of nested class have no special access to the members of the **enclosing class**
- nested classes can be forward-declared and later defined, either within the same enclosing class body, or outside of it:
    ```
    class enclose {
        class nested1; // forward declaration
        class nested2; // forward declaration
        class nested1 {}; // definition of nested class
    };
    class enclose::nested2 { }; // definition of nested class
    ```

## Local classes
Class declared inside body of a function is **local class**:
- the name of **local class** exists only in the function scope
- cannot have static data members
- **member functions** of a **local class** have **no linkage** and they need to be defined entirely inside the class body
- **local class** inside a function (including *member function*) can access the same names that the enclosing function can access