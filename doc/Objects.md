# Objects
[back to index](../README.md)

**Object** in C++ has:
- lifetime
- storage duration
- size
- type
- value
- alignemt requiremnt
- name (optionally)

## Lifetime
- every *object* and *reference* has a **lifetime**
- **lifetime** is a runtime property
  -  for any object/reference there is a point in execution of program when its **lifetime** beings and when it ends

### **Lifetime** begins when:
- the storage (with proper alignment and size) is obtained
- its initialization (if needed) is completed

[woth some minor exceptions regarding union members and arrays objects](https://en.cppreference.com/w/cpp/language/lifetime)
### **Lifetime** ends when:
- **destructor** call start for *class type* objects
- or **storage** of object is releases/reused
- or *non-class type* objects is **destroyed** (pseudo-destructors since C++20)

**Lifetime** of objest is bound by and nested in its **storage duration**.

## Storage duration
- **automatic** storage duration - allocated at the beginning of enclosing code block, deallocated at the end of code block
  - all **local** objects except those declared *static, extern, thread_local*
- **static** storage duration - allocated when the program begins execution, deallocated when program ends, only one instance of object exists
  - all objects defined at the **namespace scope**
  - objects declared with **static** or **extern**
- **dynamic** storage duration - allocation and deallocation happens per request by using **dynamic memory allocation** functions
- **thread** storage duration - allocated when the **thread** begins, deallocated when **thread** ends, each **thread** has its own instance of an object
  - objects declared **thread_local** (*static* or *extern* can appear to impact **linkage**)

## Linkage
Any **name** that denotes object, reference, function, type, template, namespace, or value, may have **linkage**.

If a **name** has **linkage**, it refers to the same **entity** as the same **name** introduced by a declaration in another **scope**

If a **name** appears in multiple scopes but does not have sufficient linkage, then several instances of the entity are generated.

- **no linkage** -  name can be referred to from current **scope**
  - **local classes** and their member functions
  - block scoped variables, not declared extern
- **internal linkage** - name can be referred to from current **translation unit**
  - variables and functions(including templates) declared with **static**
  - names declared in **unnamed namespace**
  - const variables (non-extern, non-inline, non-exported, non-template)
- **external linkage** - name can be referred to from other **translation units**
  - enums
  - functions not declared static, 
  - namespace scoped non-const variables not declared static
  - variables declared **extern**
  - **classes**, their member functions, static data members, nested classes, friend functions (first introduced with friend declaration)
  - **templates** not listed above
- **module linkage** - name can be referred to from current module
  - names declared at namespace scope have module linkage if their declarations are attached to a named module and are not exported, and don't have internal linkage

