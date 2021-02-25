# Classes
[back to index](../README.md)

## General
- **classes** and **structs** are basically the same in C++, the only difference is the default access modifier:
  - **public** for structs
  - **private** for classes

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