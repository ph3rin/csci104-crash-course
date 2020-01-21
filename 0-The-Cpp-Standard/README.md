# The Cpp Standard

## What is it?

Like many other programming languages, the C++ language is actually standardized. The C++ standard is a document that strictly defines the behavior of C++ code. 

When you write the following code:

```C++
#include <iostream>

int main() {
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
```

the C++ standard demands that the code (after complilation)  put the bytes representing `"Hello, world"` to the standard output, put an endline character to the standard output, flush it, and then return zero.

## Revisions of the Standard

C++ was first standardized back in 1998, therefore the first version of the standard is also known as C++98.

...And that was more than 20 years ago! Things have changed, of course. Over the course of the 21st century, 4 new standard revisions were made: c++03, c++11, c++14, and c++17. The current revision, c++20, will be released in the near future. As you can tell, the numbers represent years: the larger the number, the newer the standard; and the newer the standard the more language features and library features (to make your life easier).

If a compiler is capable of correcly compiling C++ code according to a specific C++ standard revision and its output demonstrates standard-compliant behavior, we say that it **supports that standard**. Usually a compiler supports more than one standard, which can be determined by compiler flags. 

For example (you might have already seen this): When compiled with flags `-std=c++11`, gcc supports the C++11 standard. 

## Undefined Behaviors

Remember from a few lines above that the C++ standards define the behavior of a C++ program? Moreover, the standard can also leave certain behaviors ***undefined***. 

Or more formally, an ***undefined behavior*** is a behavior that:

* The standard explicitly states as undefined, or
* A behavior that the standard does not explicitly define.

### What Happens if my Code Demonstrates Undefined Behavior?

Per the standard, anything can happen. A compiler can format your hard-drive or make demons fly out of your nose when it sees undefined behavior, while still being compliant to the standard.

Well, a typical compiler doesn't do the things mentioned above (because the writers of the compiler want you to use their product!) If your code has undefined behavior, it can lead to any (but not limited to) the following:

* Throws an exception.
* Terminates the program.
* Gives you seg fault.
* Spitts out undetermined values.
* Behaves as you expected.

Yes, it is allowed to behave as you expected. ...And this is actually, in most cases, the worst case, since you won't even notice that you have triggered undefined behavior!

```c++
#include <iostream>

int* foo() {
    int x = 42;
    return &x;
}

int main() {
    std::cout << *foo();
    return 0;
}
```

The above code demonstrates undefined behavior because `foo()` returns a pointer pointing to a local variable. 

However, if you compile it with a mainstream compiler (like MSVC), you will likely get the output `42`. This is the "behaves as you expected" scenario. Even so, you should never rely on undefined behavior, because you never know when it is going to break!

## Compiler Specific Extensions

Many compilers would support features beyond the c++ standard. For example, VLA (Variable-length Array) is not in any C++ standard (is in the C standard, though), but it is supported by gcc.

```c++
int main() {
    int n = 42;
    int arr[n];     // Variable-length Array used here
    return 0;
}
```

The above code would compile in gcc, but not in MSVC. Using a variable in the dimensions of an array definition is not allowed by the C++ standard.

Using such features is fine if you are only writing code to be compiled by a specific compiler, but if you want to write portable (i.e. write once, compile and run correctly everywhere), do not use such features. That is why in CSCI-104 we are not allowed to use VLA.