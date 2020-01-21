# Object Lifetime and Memory Management

## Objects

C++ is an object-oriented language. As its name suggests, it manipulates objects.

According to the C++ standard (latest draft, but the wordings should be similar):

> [**[intro.object/1]**](http://eel.is/c++draft/intro.object#1) The constructs in a C++ program create, destroy, refer to, access, and manipulate objects. An object is created **by a definition**, by **a new-expression**, when **implicitly changing the active member of a union**, or when **a temporary object is created**.

We will not cover the third scenario, but the rest are in scope of the course:

### Creation by Definition

```c++
int a;                    // (1)

int main() {
    float b;              // (2)
    return 0;
}
```

(1) creates an object of type `int`. It has the name `a`.

(2) creates an object of type `float`. It has the name `b`.

Note that if we write:

```c++
extern int a;
```

We are just writing a declaration. The object is defined and created elsewhere (if it is not then the compiler would report undefined reference).

### Create by New Expression

```c++
int main() {
    int* ptr = new int[42];       // (1)
}
```

(1) creates an unamed object with type `int[42]` (an array of `int` with size `42`).

On the same line, it creates another object (but not by new-expression!). Can you tell what it is?

### Creation of Temporary Objects

```c++
int foo() {
    return 42;
}

int main() {
    foo();              // (1)
}
```

(1) Creates a temporary object of type `int`. [[1]](#notes)

Question: does the following code create a temporary object? (Tricky question, do some research; hint: it depends on the standard revision)

```c++
int foo() {
    return 42;
}

int main() {
    int x = foo();              // (1)
}
```

## Notes

[1] We assume that integral literals (like `42`) are not implemented as temporaries.

