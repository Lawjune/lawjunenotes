## POINTERS

```cpp
#include <iostream>

int main(int argc, const char * argv[]) {
    int var = 8;
    void* ptr = &var;
    int* ptr_int = &var;
    std::cout << "ptr = " << ptr << std::endl;
    std::cout << "ptr_int = " << ptr_int << std::endl;
    
    // *ptr = 10; It doesn't work!
    *ptr_int = 10;
    std::cout << "New var = " << var << std::endl;
    
    return 0;
}
```
```output
ptr = 0x7ffee8df696c
ptr_int = 0x7ffee8df696c
New var = 10
```
*Creating memory in stack as above.*

*Creating memory in heap as below.*
```cpp
#include <iostream>

int main(int argc, const char * argv[]) {
    
    char* buffer = new char[8];
    memset(buffer, 0, 8);
    char** ptr = &buffer;
    
    std::cout << "buffer = " << buffer << std::endl;
    std::cout << "ptr = " << ptr << std::endl;
    
    delete[] buffer;
    return 0;
}
```
```output
buffer =
ptr = 0x7ffee0a0e968
```