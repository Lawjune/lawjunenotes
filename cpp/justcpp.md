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

## Strings in C++

### How Strings Work in C++ (and how to use them)

```cpp
#include <iostream>

int main(int argc, const char * argv[]) {
    
    const char* name = "Lawjune";
    std::cout << "name: " << name << std::endl;
    char name1[8] = {'L', 'a', 'w', 'j', 'u', 'n', 'e', 0};
    std::cout << "name1: " << name1 << std::endl;
    return 0;
}
```
```output
name: Lawjune
name1: Lawjune
```

```cpp
#include <iostream>
#include <string>

void print_string(const std::string& string) {
    std::cout << string << std::endl;
}

int main(int argc, const char * argv[]) {
    
    std::string name = "Lawjune";
    std::cout << "name: " << name << std::endl;
    std::cout << "name.size(): " << name.size() << std::endl;
    std::cout << "name.find(aw): " << name.find("aw") << std::endl;
    name += " hello!";
    std::cout << "name: " << name << std::endl;
    print_string(name);

    return 0;
}
```
```output
name: Lawjune
name.size(): 7
name.find(aw): 1
name: Lawjune hello!
Lawjune hello!
```

### String Literals in C++

```cpp
#include <iostream>
#include <string>
#include <stdlib.h>

int main(int argc, const char * argv[]) {
    
    char name[10] = "Law\0june";
    std::cout << name << std::endl;
    std::cout << strlen(name) << std::endl;
    name[3] = 'j';
    std::cout << name << std::endl;
    std::cout << strlen(name) << std::endl;

    return 0;
}
```
```output
Law
3
Lawjjune
8
```

```cpp
#include <iostream>
#include <string>
#include <stdlib.h>

int main(int argc, const char * argv[]) {
    
    char* name = "Lawjune";
    std::cout << name << std::endl;
    std::cout << strlen(name) << std::endl;

    return 0;
}
```
```sh
➜  welcomecpp g++ main.cpp -o main
main.cpp:7:18: warning: conversion from string literal to 'char *' is deprecated [-Wc++11-compat-deprecated-writable-strings]
    char* name = "Lawjune";
                 ^
1 warning generated.
➜  welcomecpp ./main
Lawjune
7
```

```cpp
#include <iostream>
#include <string>
#include <stdlib.h>

int main(int argc, const char * argv[]) {
    
    const char* name = "Lawjune";
    std::cout << name << std::endl;
    std::cout << strlen(name) << std::endl;
    
    const wchar_t* name1 = L"Lawjune";
    std::cout << name1 << std::endl;

    const char16_t* name2 = u"Lawjune";
    std::cout << name2 << std::endl;

    const char32_t* name3 = U"Lawjune";
    std::cout << name3 << std::endl;

    return 0;
}
```
```sh
g++ main.cpp -o main --std=c++11
```
```output
Lawjune
7
0x10bdeaf28
0x10bdeaf48
0x10bdeaf28
```

*clang does not support.*
```cpp
#include <iostream>
#include <string>
#include <stdlib.h>

int main(int argc, const char * argv[]) {
    using  namespace std::string_literals;
    
    std::u32string name = U"Lawjune"s + U" hello!";
//    std::cout << name << std::endl;
    
    const char* example = R"(line1
line2
line3
line3)";
    
    std::cout << example << std::endl;
    
    return 0;
}
```

## CONST in C++

```cpp
#include <iostream>
#include <string>

int main(int argc, const char * argv[]) {
    
    const int MAX_AGE = 100;
    int* a = new int;
    const int* b = new int;
    // int const* == const int*
    
    *a = 2;
    a = (int*)&MAX_AGE;
    std::cout << *a << std::endl;
    
    // *b = 2 // It doesn't work!
    b = (int*)&MAX_AGE;
    std::cout << *b << std::endl;
    b = nullptr;
    std::cout << b << std::endl;
    
//    delete a;
    delete b;
    
    return 0;
}
```
```output
100
100
0x0
```

```cpp
#include <iostream>
#include <string>

class Entity {
private:
    int m_x, m_y;
    mutable int var;
public:
    int get_x() const {
        
        // Can't modify the members
        // m_x = 1 -> it doesn't work!
        // Only allow to modify "mutable" variables
        var = 1;
        return m_x;
    }
    
    void set_x(int x) {
        m_x = x;
    }
};

void print_entity(const Entity& e) {
    std::cout << e.get_x() << std::endl;
}

int main(int argc, const char * argv[]) {
    
    Entity e;
    print_entity(e);
    
    return 0;
}
```

## The Mutable Keyword in C++


```cpp
#include <iostream>
#include <string>

class Entity {
private:
    std::string m_name;
    mutable int m_debug_count = 0;
public:
    const std::string& get_name() const {
        m_debug_count++;
        return m_name;
    }
};


int main(int argc, const char * argv[]) {
    
    Entity e;
    e.get_name();
    
    return 0;
}
```

## Member Initializer Lists in C++ (Constructor Initializer List)

```cpp
#include <iostream>
#include <string>

class Example {
public:
    Example()
    {
        std::cout << "Created Entity!" << std::endl;
    }
    
    Example(int x)
    {
        std::cout << "Created Entity with " << x << "!" << std::endl;
    }
};

class Entity
{
private:
    std::string m_name;
    int x, y, z;
    Example m_example;
public:
    Entity() : m_name("Unknown"), x(0), y(0), z(0)
    {
        m_example = Example(7);
    }
    
    Entity(const std::string& name) : m_name(name), m_example(6)
    {}
    
    const std::string& get_name() const
    {
        return m_name;
    }
};


int main(int argc, const char * argv[])
{
    
    Entity e;
    std::cout << e.get_name() << std::endl;

    Entity e1("Lawjune");
    std::cout << e1.get_name() << std::endl;
    
    return 0;
}
```
```output
Created Entity!
Created Entity with 7!
Unknown
Created Entity with 6!
Lawjune
```

## Ternary Operators in C++ (Conditional Assignment)

```cpp
#include <iostream>
#include <string>

static int s_level = 1;
static int s_speed = 2;

int main(int argc, const char * argv[])
{
    s_speed = s_level > 5 ? 10 : 5;
    std::cout << s_speed << std::endl;
    
    std::string rank = s_level > 10 ? "Master" : "Beginner";
    std::cout << rank << std::endl;
    
    return 0;
}
```
```output
5
Beginner
``` 

## How to CREATE/INSTANTIATE OBJECTS in C++

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    std::string m_name;
public:
    Entity() : m_name("Unknown") {}
    
    Entity(const std::string& name) : m_name(name) {}
    
    const std::string& get_name() const
    {
        return m_name;
    }
};


int main(int argc, const char * argv[])
{
    Entity* entity;
    {
        Entity e;

        std::cout << e.get_name() << std::endl;
   
//        Entity e1("Lawjune");
//        entity = &e; // Not working!
        Entity e1 = Entity("Lawjune");
        std::cout << e1.get_name() << std::endl;
      
        // Not recommemd to use new here!!!
        Entity* e2 = new Entity("Lawjune-2");
        entity = (Entity*) &e2;
        std::cout << entity->get_name() << std::endl;
        delete e2;
    }
    
    return 0;
}
```
```output
Unknown
Lawjune
@Ѐ�LawjuneLawjune
```

## The NEW Keyword in C++

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    std::string m_name;
public:
    Entity() : m_name("Unknown") {}
    
    Entity(const std::string& name) : m_name(name) {}
    
    const std::string& get_name() const
    {
        return m_name;
    }
};


int main(int argc, const char * argv[])
{
    int a = 2;
    int* b = new int[50]; // 4 * 50 = 200 bytes
    
    // Created a real object!
    Entity* e = new Entity[50];
    
    // Only allocate the memory without constructing an object
    Entity* e1 = (Entity*)malloc(sizeof(Entity));
    
    std::cout << e->get_name() << std::endl;
    std::cout << e1->get_name() << std::endl;
    
    delete[] e;
//    delete[] e1;
    delete[] b;
    
    return 0;
}
```
```output
Unknown

```


## Implicit Conversion and the Explicit Keyword in C++

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    std::string m_name;
    int m_age;
public:
    explicit Entity(int age) : m_name("Unknown"), m_age(age) {}
    
    explicit Entity(const std::string& name) : m_name(name), m_age(-1) {}
    
    const std::string& get_name() const
    {
        return m_name;
    }
};


int main(int argc, const char * argv[])
{
    Entity a("Lawjune");
    Entity b(37);
    
    std::cout << a.get_name() << std::endl;
    std::cout << b.get_name() << std::endl;
    
    return 0;
}
```
```output
Lawjune
Unknown
```

## OPERATORS and OPERATOR OVERLOADING in C++

```cpp
#include <iostream>
#include <string>

struct vector2
{
    float x, y;
    
    vector2(float x, float y) : x(x), y(y) {}
    
    vector2 add(const vector2& other) const {
//        return vector2(x + other.x, y + other.y);
        return vector2(x + other.x, y + other.y);
    }
    
    vector2 multiply(const vector2& other) const {
        return vector2(x * other.x, y * other.y);
    }
    
    vector2 operator+(const vector2& other) {
        return vector2(x + other.x, y + other.y);
    }
    
    vector2 operator*(const vector2& other) {
        return vector2(x * other.x, y * other.y);
    }
};

std::ostream& operator<<(std::ostream& stream, const vector2& other)
{
    stream << other.x << ", " << other.y;
    return stream;
}

int main(int argc, const char * argv[])
{
    vector2 position(4.0f, 4.0f);
    vector2 speed(0.5f, 1.5f);
    vector2 powerup(1.1f, 1.1f);
    
    vector2 result1 = position.add(speed.multiply(powerup));
    vector2 result2 = position.add(speed.multiply(powerup));
    vector2 result3 = position + speed * powerup;
    
    std::cout << result1 << std::endl;
    std::cout << result2 << std::endl;
    std::cout << result3 << std::endl;
    
    return 0;
}
```
```output
4.55, 5.65
4.55, 5.65
4.55, 5.65
```

## The "this" keyword in C++

```cpp
#include <iostream>
#include <string>

//void print_entity(const Entity& e);

class Entity
{
public:
    int x, y;
    
    Entity(int x, int y)
    {
        this->x = x;
        this->y = y;

//        print_entity(*this);
    }
    
    int get_x() const
    {
        const Entity& e = *this;
    }
};

void print_entity(Entity* e)
{
    // Print
}

int main(int argc, const char * argv[])
{
    
    return 0;
}

```

## Object Lifetime in C++ (Stack/Scope Lifetimes)

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    int x;
public:
    Entity()
    {
        std::cout << "Created Entiity!" << std::endl;
    }
    ~Entity()
    {
        std::cout << "Destroyed Entiity!" << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    {
//        Entity e;
        Entity* e = new Entity();
    }
    
    return 0;
}
```

***Stack-based variable***
```cpp
Entity e;
```
```output
Created Entiity!
Destroyed Entiity!
```

***Heap-based variable***
```cpp
Entity* e = new Entity();
```
```output
Created Entiity!
```
*The memory does get cleaned by the operating system when our application terminates.*

*A heap-based variable gets free and destroyed as soon as we go out of scope.*

*If you create a variable on the stack it's going to cease to exist when it goes out of start.*

```cpp
#include <iostream>
#include <string>

int* create_array()
{
//    int array[50]; -> It doesn't work!
    int* array = new int[50];
    return array;
}

void fill_array(int* array)
{
    // It does not work!
    // Because the array is in the stack!
    array[1] = 1;
}

int main(int argc, const char * argv[])
{
    int* new_array = create_array();
    std::cout << new_array[0] << std::endl;
    fill_array(new_array);
    std::cout << new_array[0] << std::endl;
    
    int array[50];
    std::cout << array[0] << std::endl;
    fill_array(array);
    std::cout << array[0] << std::endl;
    
    return 0;
}
```
```output
0
0
371929088  
371929088
```

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    int x;
    std::string name;
public:
    Entity(std::string entity_name)
    {
        name = entity_name;
        std::cout << "Created Entiity: " << name << std::endl;
    }
    ~Entity()
    {
        std::cout << "Destroyed Entiity: " << name << std::endl;
    }
};

class ScopedPtr
{
private:
    Entity* m_ptr;
public:
    ScopedPtr(Entity* ptr) : m_ptr(ptr) {}
    
    ~ScopedPtr() {
        delete m_ptr;
    }
};

int main(int argc, const char * argv[])
{
    {
        ScopedPtr e1(new Entity("e1"));
    }
    
    ScopedPtr e1(new Entity("e1"));
    
    return 0;
}
```

## SMART POINTERS in C++ 

### SMART POINTERS in C++ - std::unique_ptr

*The unique_ptr is a scope pointer. This pointer has to be unique you can't copy a unique pointer because if you copy a unique pointer the memory that it's pointing to they'll bascically you'll have two unique pointers pointing to the same block memory and when one of them dies it will free that memory.* 

```cpp
#include <iostream>
#include <string>
#include <memory>

class Entity
{
private:
    int x;
    std::string name;
public:
    Entity(std::string entity_name)
    {
        name = entity_name;
        std::cout << "Created Entiity: " << name << std::endl;
    }
    ~Entity()
    {
        std::cout << "Destroyed Entiity: " << name << std::endl;
    }
    
    void print()
    {
        std::cout << name << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    {
        // Make exception safety
        // make_unique only exists since c++14
        // std::unique_ptr<Entity> entity = std::make_unique<Entity>("entity");
        std::unique_ptr<Entity> entity(new Entity("entity"));
        entity->print();
    }
    return 0;
}
```
```output
Created Entiity: entity
entity
Destroyed Entiity: entity
```

### SMART POINTERS in C++ - std::shared_ptr

```cpp
#include <iostream>
#include <string>
#include <memory>

class Entity
{
private:
    int x;
    std::string name;
public:
    Entity(std::string entity_name)
    {
        name = entity_name;
        std::cout << "Created Entiity: " << name << std::endl;
    }
    ~Entity()
    {
        std::cout << "Destroyed Entiity: " << name << std::endl;
    }
    
    void print()
    {
        std::cout << name << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    {
        std::shared_ptr<Entity> e0;
        {
            std::shared_ptr<Entity> shared_entity(new Entity("shared_entity"));
            shared_entity->print();
            e0 = shared_entity;
            e0->print();
        }
    }

    return 0;
}
```

### SMART POINTERS in C++ - std::weak_ptr

```cpp
...
...
int main(int argc, const char * argv[])
{
    {
        std::weak_ptr<Entity> e0;
        {
            std::shared_ptr<Entity> shared_entity(new Entity("shared_entity"));
            shared_entity->print();
            std::weak_ptr<Entity> weak_entity = shared_entity;
            // weak_entity->print(); // It doesn't work!
            e0 = shared_entity;
            // e0->print(); // It doesn't work!
        }
    }

    return 0;
}
```

### Copying and Copy Constructors in C++

```cpp
#include <iostream>
#include <string>

struct vector2
{
    float x, y;
};

int main(int argc, const char * argv[])
{
    vector2* a = new vector2();
    vector2* b = a;
    b->x=2;

    std::cout << a->x << std::endl;
    return 0;
}
```
```output
2
```

```cpp
#include <iostream>
#include <string>

class String
{
private:
    char* m_buffer;
    unsigned int m_size;
public:
    String(const char* string)
    {
        std::cout << "Copy string!" << std::endl;
        m_size = (unsigned int) strlen(string);
        m_buffer = new char[m_size+1];
        memcpy(m_buffer, string, m_size+1);
        m_buffer[m_size] = 0;
    }
    
    String(const String& other) : m_size(other. m_size)
    {
        m_buffer = new char[m_size + 1];
        memcpy(m_buffer, other.m_buffer, m_size);
    }
    
    ~String()
    {
        delete[] m_buffer;
    }
    char& operator[](unsigned int index)
    {
        return m_buffer[index];
    }
    
    friend std::ostream& operator<<(std::ostream& stream, const String& string);
};

std::ostream& operator<<(std::ostream& stream, const String& string)
{
    stream << string.m_buffer;
    return stream;
}

void print_string(const String& string)
{
    std::cout << string << std::endl;
}

int main(int argc, const char * argv[])
{
    String string = "Lawjune";
    String second = string;
    second[2] = 'a';
//    std::cout << string << std::endl;
//    std::cout << second << std::endl;
    print_string(string);
    print_string(second);
    return 0;
}
```
```output
Copy string!
Lawjune
Laajune
```

### The Arrow Operator in C++

```cpp
#include <iostream>
#include <string>

class Entity
{
public:
    void print() const
    {
        std::cout << "Hello!" << std::endl;
    }
};

class ScopedPtr
{
private:
    Entity* m_obj;
public:
    ScopedPtr(Entity* entity) : m_obj(entity) {}
    ~ScopedPtr() { delete m_obj; }
    Entity* operator->() { return m_obj; }
    const Entity* operator->() const { return m_obj; }
    
};

int main(int argc, const char * argv[])
{
    Entity e;
    e.print();
    
    Entity* ptr = &e;
    Entity& entity = *ptr;
    (*ptr).print();
    ptr->print();
    entity.print();
    
    const ScopedPtr ptr_entity = new Entity();
    ptr_entity->print();
}
```
```output
Hello!
Hello!
Hello!
Hello!
Hello!
```
```cpp
#include <iostream>
#include <string>

struct vector3
{
    float x, y, z;
    
};


int main(int argc, const char * argv[])
{
    int offset = (int)(size_t)&((vector3*)nullptr)->z;
    std::cout << offset << std::endl;
    
    return 0;
}
```
```output
8
```

## Containers: std:vector

### Dynamic Arrays in C++

```cpp
#include <iostream>
#include <string>
#include <vector>

struct Vertex
{
    float x, y, z;
};

std::ostream& operator<<(std::ostream& stream, const Vertex& vertex)
{
    stream << vertex.x << ", " << vertex.y << ", " << vertex.z;
    return stream;
}

int main(int argc, const char * argv[])
{
    std::vector<Vertex> vertices;
    vertices.push_back((Vertex){1, 2, 3});
    vertices.push_back((Vertex){4, 5, 6});
    for (int i = 0; i < vertices.size(); i++)
        std::cout << vertices[i] << std::endl;
    for (Vertex& v: vertices)
        std::cout << v << std::endl;
    vertices.erase(vertices.begin() + 1);
    for (Vertex& v: vertices)
        std::cout << v << std::endl;
    return 0;
}
```
```output
1, 2, 3
4, 5, 6
1, 2, 3
4, 5, 6
1, 2, 3
```

### Optimizing the usage of std::vector in C++

--> Construct the vertex in the same place as it will be stored. Rather than constructing it in the current method and then copying it to the vertex location.
--> use emplace_back rather than push_back and only pass the parameter list for the constructor.

```cpp
#include <iostream>
#include <string>
#include <vector>

struct Vertex
{
    float x, y, z;
    
    Vertex(float x, float y, float z) : x(x), y(y), z(z) {}

    Vertex(const Vertex& vertex) : x(vertex.x), y(vertex.y), z(vertex.z)
    {
        std::cout << "Copied! " << vertex.x << " at " << &vertex << std::endl;
    }
};


int main(int argc, const char * argv[])
{
    std::vector<Vertex> vertices;
//    vertices.reserve(3);
    vertices.push_back(Vertex(1, 2, 3));
    vertices.push_back(Vertex(4, 5, 6));
    vertices.push_back(Vertex(7, 8, 9));
    return 0;
}
```
```output
Copied! 1 at 0x7ffeebb77948
Copied! 4 at 0x7ffeebb77930
Copied! 1 at 0x7f9d48c05940
Copied! 7 at 0x7ffeebb77920
Copied! 4 at 0x7f9d48c059fc
Copied! 1 at 0x7f9d48c059f0
```

**Optimized**
```cpp
int main(int argc, const char * argv[])
{
    std::vector<Vertex> vertices;
    vertices.reserve(3);
    vertices.push_back(Vertex(1, 2, 3));
    vertices.push_back(Vertex(4, 5, 6));
    vertices.push_back(Vertex(7, 8, 9));
    return 0;
}
```
```output
Copied! 1 at 0x7ffee1d97940
Copied! 4 at 0x7ffee1d97930
Copied! 7 at 0x7ffee1d97920
```

## Using Libraries in C++

### Using Libraries in C++ (Static Linking)

*Download the pre-compiled binaries from https://www.glfw.org/download, extract and copy to the development project directory.*


### Using Dynamic Libraries in C++

### Making and Working with Libraries in C++ (Multiple Projects in Visual Studio)

https://blog.ntechdevelopers.com/setup-opengl-environment-on-xcode/

Preparing Libraries:
CMake:
Since most of the libraries provide cmake files to generate files, it is better to have a CMake on your Mac. I do not know a lot about CMake. I just explain how to install it.

For convenience, I installed CMake by Homebrew. Here is the link for installing Homebrew:http://brew.sh
After installing Homebrew, just type “brew install cmake” command in Terminal and CMake will be installed.

GLFW:
1. Go to website and download the file: http://www.glfw.org
2. Unzip the downloaded file.
3. Open Terminal and go to the root directory of glfw, like “glfw-3.2”.
4. Type commands:
cmake .
make
sudo make install
It means GLFW is successfully installed.

GLEW:
1. Go to website and download the file:http://glew.sourceforge.net
2. Open Terminal and go to the root directory of glew, like “glfw-3.1.2”.
3. Type commands:
make
make install
make clean
You may have problem like “no permission”. Because users do not have the permission to directly modify the folder /usr/local/include and /usr/local/lib. You may use command in Terminal to get the permission if you like to install in these folders. Otherwise you can modify the Makefile so that it will generate into different folder. The commands to get the permission are
sudo chown -R $(whoami) /usr/local/include/GL
sudo chown -R $(whoami) /usr/local/lib

What’s more, you can also install glew by Homebrew.


Build in Xcode
1. Create a new Xcode project
2. Choose OSX->Application->Command Line Tool. Then give a name and path for this project.
3. Add framework.
a. click project name -> Build Phases -> link binary with libraries
b. Add these framework by click “+”:
OpenGL.framework
IOKit.framework
CoreVideo.framework
Cocoa.framework
c. Add extra library. Click “Add Other…”, use shortcuts “command+shift+G”, and input path “/usr/local/lib”
(If you do not change the path while installing, you will find all required library here). Add this library in:
libglfw3.a
libGLEW.a
4. Add header and library path.
a. Go to “Build Settings”.
b. Find “Header Search Path”. Input “/usr/local/include” (or the other folder contains the header)
c. Find “Library Search Path”. Input “/usr/local/lib” (or the other folder contains the header)

Since GLFW is supported by these framework on Mac, we need to include four frameworks in Step 3. However, from GLFW website:

If you are using the dynamic library version of GLFW, simply add it to the project dependencies.
If you are using the static library version of GLFW, add it and the Cocoa, OpenGL, IOKit and CoreVideo frameworks to the project as dependencies. They can all be found in /System/Library/Frameworks.
Other Libraries
GLM:
1. Go to website and download: http://glm.g-truc.net/0.9.7/index.html
2. Unzip downloaded file.
3. Go to “Build Settings” in project on Xcode. Find “Header Search Path”. Input “/<root directory of glm>”
GLM just needs to be included in the project. You can also copy “/<root directory of glm>/glm” folder to other place and include that path in the project. I just copy it into my “/usr/local/include”. It is convenient for me to organize it.

SOIL:
SOIL is a library to import pictures. It supports several types of pictures. Since the latest version is 07-07-2008, to make it work, I took much time to build it up.
1. Go to the website and download the “old” latest version http://www.lonesock.net/soil.html.
2. Unzip downloaded file.
3. Go to the root directory of SOIL.
4. Edit Makefile.
a. Add “-m64” after CFLAGS. Then this line become “CFLAGS += -c -O2 -Wall -m64”
(Resource: http://stackoverflow.com/a/35862048)
b. Modify “INCLUDEDIR” to the folder that you want to put in the header. For example, mine is “/usr/local/include/SOIL”.
c. Modify “LIBDIR” to the folder that you want to put in the library. For example, mine is “/usr/local/lib”.
d. Use Terminal to the root directory of SOIL. Type command
make
make install
make clean
e. Go to Build Phases -> link binary with libraries in project. Add other -> find “libSOIL.a”.
























