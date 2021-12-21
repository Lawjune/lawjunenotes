## POINTERS & REFERENCES

### POINTERS in C++

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

### REFERENCES in C++

```cpp
#include <iostream>

void increament_ptr(int* value)
{
    (*value)++;
}

void increament_ref(int& value)
{
    value++;
}

int main(int argc, const char * argv[]) {
    int a = 5;
    int* b = &a;
    int& ref = a;
    
    std::cout << "b = " << b << std::endl;
    std::cout << "ref = " << ref << std::endl;
    
    ref = 2;
    std::cout << "now ref = " << ref << " just an alias of a" << std::endl;
    
    increament_ptr(&a);
    std::cout << "a = " << a << std::endl;
    std::cout << "b = " << b << std::endl;
    std::cout << "ref = " << ref << std::endl;
    
    increament_ref(a);
    std::cout << "a = " << a << std::endl;
    std::cout << "b = " << b << std::endl;
    std::cout << "ref = " << ref << std::endl;
    
    return 0;
}
```
```output
b = 0x7ffee1b9396c
ref = 5
now ref = 2 just an alias of a
a = 3
b = 0x7ffee1b9396c
ref = 3
a = 4
b = 0x7ffee1b9396c
ref = 4
```

## CLASSES in C++

### Classes Introduction

```cpp
#include <iostream>

class Player {
    int x, y;
    int speed;
    
public:
    int get_x() {
        return x;
    }
    
    int get_y() {
        return y;
    }
    
    void move(int xa, int ya) {
        x += xa;
        y += ya;
    }
};

int main(int argc, const char * argv[]) {
    
    Player player;

    std::cout << "player.x = " << player.get_x() << std::endl;
    std::cout << "player.y = " << player.get_y() << std::endl;
    
    player.move(6, 7);
    std::cout << "player.x = " << player.get_x() << std::endl;
    std::cout << "player.y = " << player.get_y() << std::endl;
    
    return 0;
}
```
```output
player.x = 0
player.y = 0
player.x = 6
player.y = 7
```

### CLASSES vs STRUCTS in C++

* *class implicts private*
* *struct implicts public*

***"Use class if the class has an invariant; use struct if the data members can vary independently."***

***Never use inheritance of struct.***

### How to Write a C++ Class

***Just a fair enough clean code, not the final code!!!**

```cpp
#include <iostream>

class Log {
public:
    const int log_level_error = 0;
    const int log_level_warning = 1;
    const int log_level_info = 2;
    
private:
    int m_log_level = log_level_info; // m means member
    
public:
    void set_level(int level) {
        m_log_level = level;
    }
    
    void error(const char* message) {
        if (m_log_level < log_level_warning)
        std::cout << "[Error]: " << message << std::endl;
    }
    
    void warn(const char* message) {
        if (m_log_level >= log_level_warning)
        std::cout << "[Warning]: " << message << std::endl;
    }
    
    void info(const char* message) {
        std::cout << "[Info]: " << message << std::endl;
    }
};


int main(int argc, const char * argv[]) {
    

    
    Log log;
    log.set_level(log.log_level_warning);
    log.error("Error!");
    log.warn("Warning!");
    log.info("Info!");
    
    return 0;
}
```

## Static in C++

### Static for Classes and Structs in C++

```cpp
#include <iostream>

struct Entity {
    static int x, y;
    int a, b;
    void print() {
        std::cout << x << ", " << y << std::endl;
    }
    
    static void Print() {
        // The static method can not access to the instance variables such a, b
        // std::cout << a << ", " << b << std::endl;
        std::cout << x << ", " << y << std::endl;
    }
};

int Entity::x;
int Entity::y;

int main(int argc, const char * argv[]) {
    
    Entity e;
    e.x = 6;
    e.y = 7;
    
    Entity e1;
    e1.x = 16;
    e1.y = 17;
    
    e.print();
    
    Entity::x = 26;
    Entity::y = 27;
    e.print();
    e.Print();
    
    return 0;
}
```
```output
16, 17
26, 27
26, 27
```

### Local Static in C++

```cpp
#include <iostream>

void func() {
    static int i = 0;
    i++;
    std::cout << i << std::endl;
}

int main(int argc, const char * argv[]) {
    
    func();
    func();
    func();
    func();
    func();
    func();
    
    return 0;
}
```
```output
1
2
3
4
5
6
```

```cpp
#include <iostream>

class Singleton {
private:
    static Singleton* s_instance;
public:
    static Singleton& get() { return *s_instance; }
    void say_hello() { printf("Hello!\n"); }
};

Singleton* Singleton::s_instance = nullptr;

int main(int argc, const char * argv[]) {
    
    Singleton::get().say_hello();
    
    return 0;
}
```
==(**Equals**)
```cpp
#include <iostream>

class Singleton {
public:
    static Singleton& get() {
        static Singleton instance;
        return instance;
    }
    void say_hello() { printf("Hello!\n"); }
};

int main(int argc, const char * argv[]) {
    
    Singleton::get().say_hello();
    
    return 0;
}
```

### ENUMS in C++

```cpp
#include <iostream>

enum enum_example {
    A, B, C
};

enum enum_char : unsigned char {
    D, E, F
};

int main(int argc, const char * argv[]) {
    
    enum_example enum_value = B;
    std::cout << "enum_value = " << enum_value << std::endl;
    
    enum_char enum_char_value = E;
    std::cout << "enum_char_value = " << enum_char_value << std::endl;
    
    return 0;
}
```
```output
enum_value = 1
enum_char_value =
```

```cpp
#include <iostream>

class Log {
public:
//    const int log_level_error = 0;
//    const int log_level_warning = 1;
//    const int log_level_info = 2;
    enum level_enum {
        log_level_error = 0, log_level_warning, log_level_info
    };
    
private:
    level_enum m_log_level = log_level_info; // m means member
    
public:
    void set_level(level_enum level) {
        m_log_level = level;
    }
    
    void error(const char* message) {
        if (m_log_level < log_level_warning)
        std::cout << "[Error]: " << message << std::endl;
    }
    
    void warn(const char* message) {
        if (m_log_level >= log_level_warning)
        std::cout << "[Warning]: " << message << std::endl;
    }
    
    void info(const char* message) {
        std::cout << "[Info]: " << message << std::endl;
    }
};


int main(int argc, const char * argv[]) {
    

    
    Log log;
    log.set_level(log.log_level_warning);
    log.error("Error!");
    log.warn("Warning!");
    log.info("Info!");
    
    return 0;
}
```
```output
[Warning]: Warning!
[Info]: Info!
```

### Constructors in C++

```cpp
#include <iostream>

class Entity {
public:
    float x, y;
    
    Entity() {
        x = 0.0f;
        y = 0.0f;
    }
    
    Entity(float a, float b) {
        x = a;
        y = b;
    }
    
    void print() {
        std::cout << x << std::endl;
    }
};

int main(int argc, const char * argv[]) {

    Entity e;
    e.print();
    
    Entity e1(10.0f, 5.0f);
    e1.print();
    return 0;
}
```
```output
0
10
```

### Destructors in C++

```cpp
#include <iostream>

class Entity {
public:
    float x, y;
    
    Entity() {
        x = 0.0f;
        y = 0.0f;
    }
    
    Entity(float a, float b) {
        x = a;
        y = b;
    }
    
    ~Entity() {
        std::cout << "Destroyed Entity with sum: " << (x + y) << std::endl;
    }
    
    void print() {
        std::cout << (x + y) << std::endl;
    }
};

void func() {
    Entity e(6.0f, 7.0f);
    e.print();
}

int main(int argc, const char * argv[]) {

    Entity e;
    e.print();
    
    func();
    
    Entity e1(10.0f, 5.0f);
    e1.print();
    
    return 0;
}

```
```output
0
13
Destroyed Entity with sum: 13
15
Destroyed Entity with sum: 15
Destroyed Entity with sum: 0
```

### Inheritance in C++

```cpp
#include <iostream>

class Entity {
public:
    float x, y;
    
    Entity() {
        x = 0.0f;
        y = 0.0f;
    }
    
    void move(float xa, float ya) {
        x += xa;
        y += ya;
        std::cout << "Now moved to { " << x << " , " << y << " }." << std::endl;
    }
};

class Player : public Entity {
public:
    const char* name;
};

int main(int argc, const char * argv[]) {
    
    std::cout << sizeof(Entity) << std::endl;
    std::cout << sizeof(Player) << std::endl;
    
    Player player;
    player.move(6, 7);
    return 0;
}
```
```output
8
16
Now moved to { 6 , 7 }.
```

## Virtual Functions 

### Virtual Functions in C++

https://pabloariasal.github.io/2017/06/10/understanding-virtual-tables/

```cpp
#include <iostream>
#include <string>

class Entity {
public:
    virtual std::string get_name() { return "Entity"; }
};

class Player : public Entity {
private:
    std::string m_name;
public:
    Player(const std::string& name) : m_name(name) {}
    std::string get_name() override { return m_name; }
};

int main(int argc, const char * argv[]) {
    
    Entity* e = new Entity();
    std::cout << e->get_name() << std::endl;
    
    Player* p = new Player("Lawjune");
    std::cout << p->get_name() << std::endl;
    
    Entity* entity = p;
    std::cout << entity->get_name() << std::endl;
    
    return 0;
}
```
```output
Entity
Lawjune
Lawjune
```

### Interfaces in C++ (Pure Virtual Functions)

```cpp
#include <iostream>
#include <string>

class Printable {
public:
    virtual std::string get_class_name() = 0;
};

class Entity : public Printable {
public:
    virtual std::string get_name() { return "Entity"; }
    std::string get_class_name() override { return "Entity"; }
};

class Player : public Entity {
private:
    std::string m_name;
public:
    Player(const std::string& name) : m_name(name) {}
    std::string get_name() override { return m_name; }
    std::string get_class_name() override { return m_name; }
};

void print(Printable* obj) {
    std::cout << obj->get_class_name() << std::endl;
}

int main(int argc, const char * argv[]) {
    
    Entity* e = new Entity();
    std::cout << e->get_name() << std::endl;
    
    Player* p = new Player("Lawjune");
    std::cout << p->get_name() << std::endl;
    
    Entity* entity = p;
    std::cout << entity->get_name() << std::endl;
    
    print(p);
    print(e);
    
    return 0;
}
```
```output
Entity
Lawjune
Lawjune
Lawjune
Entity
```

## Visibility in C++

## Arrays in C++

```cpp
#include <iostream>

int main(int argc, const char * argv[]) {
        
    int example[5];
    int* ptr = example;
    for (int i=0; i<5; i++)
        example[i] =6;
    
    example[2] = 7;
    *(int*)((char*)ptr + 8) = 6;
    
    return 0;
}
```

```cpp
#include <iostream>

class Entity {
public:
    static const int exampleSize = 5;
    int example[exampleSize];
    Entity() {
        for (int i=0; i < exampleSize; i++)
            example[i] = 6;
    }
};

int main(int argc, const char * argv[]) {
        

    Entity e;
    for (int i=0; i<5; i++) {
        std::cout << e.example[i] << " " << std::endl;
    }
    
    int* another = new int[5];
    for (int i=0; i < 5; i++)
        another[i] = 7;
    delete[] another;
    
    return 0;
}
```

























