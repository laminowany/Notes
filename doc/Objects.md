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

