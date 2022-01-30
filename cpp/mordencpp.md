# 01 Heap, Stack and RALL: How does C++ manage resources

## 1.1 Basic Concepts

***heap*** != the heap in data structure

*The heap is a memory used by programming languages to store global variables.*
*By default, all global variable are stored in heap memory space. It supports Dynamic memory allocation.*

*The heap is not managed automatically for you and is not as tightly managed by the CPU. It is more like a free-floating region of memory.*

```cpp
new delete => free store
```
```c
malloc free => heap
``` 

***stack***

*A stack is a special area of computer's memory which stores temporary variables created by a function. In stack, variables are declared, stored and initialized during runtime.*

*It is a temporary storage memory. When the computing task is complete, the memory of the variable will be automatically erased*

https://www.guru99.com/stack-vs-heap.html#:~:text=A%20stack%20is%20a%20special,variable%20will%20be%20automatically%20erased.

***RALL***

*Resource Acquisition Is Initialization or RAII, is a C++ programming technique which binds the life cycle of a resource that must be acquired before use (allocated heap memory, thread of execution, open socket, open file, locked mutex, disk space, database connection—anything that exists in limited supply) to the lifetime of an object.*

## 1.2 Heap

```cpp
auto ptr = new std::vector<int>();
```

```java
ArrayList<int> list = new ArrayList<int>();
```

```cpp
lst = list()
```

*In some safety areas, dynamically allocating memory is forbitten, for example airplane, tele-devices, etc.*

**Three steps:***
1. Allocate a particular memory
2. Free the allocated memory
3. Find and free the the no-long-used memory

C++: 1, 2
Java: 1, 2 ,3
Python: 1, 2, 3

***All of steps are connected!**
1. Request Memory
	- How much memory have not been allocated
	- Request new memory from OS
	- Mark the used memory
	- NPay attention to garbage collection
2. Release Memory
	- Not only mark the memory as unused
	- Need to make the unused memory continous as much as possible
	- Current programming mode needs the memory request as continous
3. Garbage Collection
	- Many strategies and methods
	- Balance of performance, real-time and extra assumptions

**Example**
Free memory address point ->

a. A memory block with length as 8 
->[unused][unused][unused][unused][unused][unused][unused][unused]

b. Allocated 1 unit
[used-1]->[unused][unused][unused][unused][unused][unused][unused]

c. Allocated 2 units and 1 unit
[used-1][used-2][used-2][used-3]->[unused][unused][unused][unused]

d. Released the 2nd 2 units
[used-1][unused][unused][used-3]->[unused][unused][unused][unused]
		|---Fragment---|

e. Released the 3rd 1 unit without merging
[unused][unused][unused][unused]->[unused][unused][unused][unused]
*Note: OS Memory Management can not meet the requirement of >4 units memory request!*

f. Merge the free memory blocks => OS Memory Management handles it!
[used-1]->[unused][unused][unused][unused][unused][unused][unused]

***Use the `new` and `delete` correctly!***

**Memory Leaking Example**

```cpp
void foo()
{
  bar* ptr = new bar();
  ...
  ...
  delete ptr;
}
```
- *The `...` codes might throw exceptions to cause that `delete ptr` not been executed!*
- *It's not a C++ way! It should use `stack` rather than `heap` for memory allocation in this case of 99% possibilities.*

***The Better Solution***
```cpp

bar* make_bar(…)
{
  bar* ptr = nullptr;
  try {
    ptr = new bar();
    ...
  }
  catch (...) {
    delete ptr;
    throw;
  }
  return ptr;
}

void foo()
{
  ...
  bar* ptr = make_bar(…)
  ...
  delete ptr;
}
```

## 1.3 Stack

*Usually for local variables.*

```cpp

void foo(int n)
{
  ...
}

void bar(int n)
{
  int a = n + 1;
  foo(a);
}

int main()
{
  ...
  bar(42);
  ...
}
```

a. Before bar() executed 
[unused][unused][unused][unused][unused][unused][unused]->[main used]

b. Called bar()
[unused][unused][unused][unused][unused]->[return to main address][bar_param: 42][main used]

c. Before foo() executed 
[unused][unused][unused]->[a = 43][register reserved space][return to main address][bar_param: 2][main used]

d. Called foo
<-[available space for foo][return to bar address][foo_param: 43][a = 43][register reserved space][return to main address][bar_param: 2][main used]

- *Stack addressing: from buttom to top.*
- *Put parameters into stack while calling function - Ignore the details of passing parameters by resgisters.*
- *Put the address of next `assembly instruction` into stack and jump to the new function.*
- *Entered into the new function:*
	- *Save context.*
	- *Adjust stack-point to allocate memory for local variables.*
	- *Execute function.*
	- *Return to the caller function address.*
- *The memory will be released automatically in stack while the function completed.*

***Summary***
- Allocating stack memory is simple - just moving the stack-pointer.
- Releasing stack memory is simple too - just moving the stack-point post function completed.
- LIFO(Last-In-First-Out) structure will never ever have memory fragment.

*Note: The occupied stack-memory has a term called `stack frame`, therefore gcc and clang have some command line options mentioned the this `frame`, e.g. `-fomit-frame-pointer`.* 

***Importance***
*Compiler will call the desconstructor function automatically, included the function execution exception. => `stack unwinding`.*

```MSVC-report-not-used-EHse-parameter
warning C4530: C++ exception handler used, but unwind semantics are not enabled. Specify /EHsc
```

```c

#include <stdio.h>

class Obj {
public:
  Obj() { puts("Obj()"); }
  ~Obj() { puts("~Obj()"); }
};

void foo(int n)
{
  Obj obj;
  if (n == 42)
    throw "life, the universe and everything";
}

int main()
{
  try {
    foo(41);
    foo(42);
  }
  catch (const char* s) {
    puts(s);
  }
}
```
```output
Obj()
~Obj()
Obj()
~Obj()
life, the universe and everything
```
***Whatever throwing the exceptions, the desconstructor will be executed.***

## 1.4 RALL

C++ supports to store object in `stack`, but mostly objects should not and could not be stored in `stack`, because:
- Object is too big.
- Object can not be resized during compling.
- Object is a return value of funciton, but can not return the value of object.

**Object Slicing Error Example**
```cpp

enum class shape_type {
  circle,
  triangle,
  rectangle,
  …
};

class shape { … };
class circle : public shape { … };
class triangle : public shape { … };
class rectangle : public shape { … };

shape* create_shape(shape_type type)
{
  …
  switch (type) {
  case shape_type::circle:
    return new circle(…);
  case shape_type::triangle:
    return new triangle(…);
  case shape_type::rectangle:
    return new rectangle(…);
  …
  }
}
```
*Actually `create_shape` would fail to return the correct object due to the `object copy` error.*

**A better solution**
```cpp

class shape_wrapper {
public:
  explicit shape_wrapper(
    shape* ptr = nullptr)
    : ptr_(ptr) {}
  ~shape_wrapper()
  {
    delete ptr_;
  }
  shape* get() const { return ptr_; }
private:
  shape* ptr_;
};

void foo()
{
  …
  shape_wrapper ptr_wrapper(
    create_shape(…));
  …
}
```

**The jobs of compile for `new` a object and `delete` a point.**
```cpp

// new circle(…)
{
  void* temp = operator new(sizeof(circle));
  try {
    circle* ptr =
      static_cast<circle*>(temp);
    ptr->circle(…);
    return ptr;
  }
  catch (...) {
    operator delete(ptr);
    throw;
  }
}
```
```cpp
if (ptr != nullptr) {
  ptr->~shape();
  operator delete(ptr);
}
```

```cpp
~shape_wrapper()
```
=> *The basic RALL usage, not only for memory release, also included:*
- *Close file (such as fstream desconstructor)*
- *Release synchronized lock*
- *Release other important system resource*

```cpp

std::mutex mtx;

void some_func()
{
  std::lock_guard<std::mutex> guard(mtx);
  // Synchronizing work...
}
```

***Never ever:***
```cpp
std::mutex mtx;

void some_func()
{
  mtx.lock();
  // Synchronizing work...
  // Return if exception
  // The following codes would NOT be executed
  mtx.unlock();
}
```

## 1.5 References

https://en.wikipedia.org/wiki/Memory_management

https://en.wikipedia.org/wiki/Stack-based_memory_allocation

https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization

https://en.wikipedia.org/wiki/Call_stack


## 1.6 Q&A

- **Static Variables Memory Area?***
	- Not heap neither not stack.
	- Fixed memory address during programs compiled and linked.
	- Some OS have address-distorsion-algorithm for security purpose.
	- Heap and stack variables are dynamic without fixed address.

- **thread_local variables?***
	- Similiar with static variables.
	- Each thread has its single owned memory block.