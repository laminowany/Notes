# Threading and Concurrency
[back to index](../README.md)
## General
* since **C++11** we got support for **threads** and **concurrency** built in language
  
## Threading
### General
* threading model in C++ is **1:1** threading model, which means: 
  * each C++ thread (`std:thread`) corresponds to single OS thread
  * those threads are managed directly by OS scheduler
  * there is no overhead of any thread scheduler on C++ level (as oppose to using **green threads** model in different languages)
  * OS threads are not the cheapest to create and they contest for CPU which involves context switching, therefore spawning many of them or continuosly spawning short-lived threads is probably not the best idea - use **thread pool** instead
* every thread must have initial function, `std::thread` takes callable in constructor as an argument
* `std::thread` is movable but not copyable, two `std::threads` objects cannot point to the same OS thread
* thread is being spawned (**forks**) by calling `std::thread` constructor, and it's immediately ready to start executing
* every `std::thread` that was spawned must be either **joined** (`.join()`) or **detached** (`.detach()`) before `std::thread` goes out of scope and it's **dectructor** is called; otherwise the desctructor will call `std::terminate()`
* `.joinable() -> bool` indicates if thread object identifies an active thread of execution; only threads that are **joinable** can be **joined** or **detached**
* calling `.join()` blocks and waits for a given thread to finish it's execution, it does the cleanup and after function returns there is no longer any OS thread connected with given `std::thread` object; therefore it's no longer **joinable**
* **detaching** a thread (`.detach()`) creates a deamon thread that runs in background: 
  * it is irreversible operation 
  * entire communication with thread is lost
  * there is no way to bind back to that thread
* **arguments** passed to `std::thread` **constructor** are passed **by value** into `std::thread` object, then after **undetermined time** they are passed to initial function for thread - care about dangling pointers
* arguments of `std::thread` constructor are captured on the same basis as `std::bind()` does it, to pass a reference use `std::ref()`, member functions can be used in similar manner (as for `std::bind()`)
* passing reference to `std::thread` is a common way to return a value from thread
* `std::thread::hardware_concurrency()` returns the number available of hardware threads (CPU cores), if no information is available then it returns 0
  * CPU vendors usually recommend using their own libraries to get number of cores, but CDPR listened to them and look what happened with Cyberpunk (*points AMDGPUOpen*)
* there is `std::thread::id` class to identify threads and represent **id**, use
  * `.get_id()` member function per given thread object
  * static function `std::this_thread::get_id()` from *inside* the thread

#### Mutual exclusions
* aquiring **mutex** is expensive operation, use it wisely for minimal amount of code
* `std::mutex `class with member functions:
  * `.lock()` - locks the mutex, blocks if the mutex is not available
  * `.try_lock()` - tries to lock the mutex, returns if the mutex is not available
  * `.unlock()`
* `std::mutex` can be locked only once at a time from a given thread, locking it more than once from the same thread results in **UB**
* `std::recursive_mutex` can be locked multiple times, but rethink your architecture if you need it
* prefer RAII wrapper `std::scoped_lock<>` than raw `std::mutex`
  * `std::scoped_lock<>` can lock multiple mutexes at once just fine, 
  * before **C++17** there is  `std::lock_quard<>` and `std::lock(mutex1, mutex2...)` template function for locking multiple mutexes at once
* for more flexibility but with extrea cost use `std::unique_lock<>`:
  * supports **lazy lock** with `std::defer_lock`, as well as `std::adopt_lock` for already locked mutexes
  * allows to pass mutex arround between functions and transfer ownership (it's **movable** but not copyable)
  * **tracks ownership** of `std::mutex`, if unlocked manually it won't unlock it again on destruction
* for better granulatity of lock there is `std::shared_mutex` since **C++17**
  * it provides **2 levels of access**:
    * **shared** - several threads can share ownership of the same mutex
    * **exclusive** - only one thread can own the mutex
  - if one thread has acquired the **exclusive lock**, no other threads can acquire any lock
  - if one thread has acquired the **shared lock**, no other thread can acquire the **exclusive lock**
  - `std::shared_mutex` is especially useful when shared data can be safely read by any number of threads simultaneously, but a thread may only write the same data when no other thread is reading or writing at the same time
  - as **RAII wrapper** there is `std::shared_lock` which acquires lock on **shared** level






To provide mutual exclusion for somethings that happens only once (like **initialization**) 
- there is `std::call_once()` with `std::once_flag` :
```
std::once_flag flag;
std::call_once(flag, function...);
```
- or **scoped static initialization** which is **thread-safe** since **C++11**
```
{
  static MyClass instance;
}
```