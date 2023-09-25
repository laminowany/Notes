# OOP

[back to index](.././INDEX.md)

## Misc

Interesting look into OOP is thinking of derived classes as libraries, which all have the same API - defined by base class. Derived classes provide implementations of these libraries.

Libraries (objects) can implement and extend this API:

- compile time (by type of derived object)
- runtime (by state of derived object)

## Design and implementation guidelines
- [C35](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#c35-a-base-class-destructor-should-be-either-public-and-virtual-or-protected-and-non-virtual) - make destructor of base class either 
  - virtual and public or
  - non-virtual and protected
- derived objects should be subtypes, they should obey **Liskov substitution rule** and be semantically identical
- derived class can provide *more* and require *less* but not the other way around, to not break the contract from base class
- **public inheritance** models **is-a**, dont use it for code reuse but for code to be reused
- consider making **non-leaf classes** *abstract*
- consider **NVI** (non-virtual interface idiom)
- don't mix **overloading** and **overriding** 
- don't use **default parameters** in function overrides, compiler will always use the default param from base class at compilation time
- virtual functions cannot be resolved in **constructor** and **destructor**, **this** will always have type of current class, dont call any virtual from there
- **downcasting** can be replaced by changing interface in base class