# Lvalues and rvalues: a friendly definition

**A lvalue is something that points to a specific memory location.**
- live a longer life since they exist as variables
- as containers

**A rvalue is something that does not point to a anyway.**
- temporary and short-lived
- as things contained in the container

```cpp
int x = 666; // ok
```
Here `666` is an rvalue; a number (tech  a literal constant) has no specfic memory address, except for some temporary register while the program is running.

That number is assigned to `x`, which is a variable. A variable has a specfic memory location, so it is a lvalue.


```cpp
int * y = &x; // ok
```

Here we are grabb the memory address of `x` and puting it into `y`, through the **address-of operator `&`**. It takes a lvalue argument and produces an rvalue.

This is another perfectly legal operation: on the left side of the assignment we have an lvalue (a variable), on the right side a rvalue produced by the **address-of operator `&`**.

**Error operation**
```cpp
int = y;
666 = y; // error
```
```gcc
error: lvalue required as left operand of assignment
```

**Error operation**
```cpp
int * y = &666; // error
```
```gcc
error: lvalue required as unary '&' operand
```

# Functions returning lvalues and rvalues

```cpp
int set_value()
{
	return 6;
}

// ... somewhere in main() ...

set_value() = 3; // error
```

```cpp
int global = 100;

int& set_global()
{
	return global;
}

// ... somewhere in main() ...

set_global() = 400; // ok
```

# Lvalue to rvalue conversion

```cpp
int x = 1;
int y = 3;
int z = x + y;
```
`x` and `y` have undergone an implict **lvaue-to-rvalue conversion**.

# Lvalue references

An rvalue can **NOT** be converted to lvalue. *It's not a technical limitation, though: it's the programming language that has been designed that way.*

```cpp
int y = 10;
int& yref = y;
yref++; 		// y is now 11
```

```cpp
int& yref = 10;  // error
```

```cpp
void func(int& x)
{
}

int main()
{
	func(10); // Nope!

	// This works instead:
	// int x = 10;
	// func(x);
}
```


# Const lvalue reference to the rescue

That's what GCC would say about the last two code snippets:
```gcc
error: invalid initialization of non-const reference of type 'int&' from an rvalue of type 'int'
```

GCC complains about the reference not being **const**, namely a constant. According to the language specifications, you are allowed to bind a const lvalue to an rvalue. So the following snippet works like a charm:
```cpp
const int& ref = 10; // ok
```

```cpp
void func(const int& x)
{
}

int main()
{
	func(10); // ok
}
```

```cpp
// the following...
const int& ref = 10;

// ... would translate to:
int __internal_unique_name = 10;
const int& ref = __internal_unique_name;
```

```cpp
const int& ref = 10;
std::cout << ref << "\n";   // OK!
std::cout << ++ref << "\n"; // error: increment of read-only reference ‘ref’
```

























































