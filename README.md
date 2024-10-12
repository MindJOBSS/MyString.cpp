# MyString.cpp
This String class is a custom implementation of a string-like object, providing similar functionality to std::string but with manually managed dynamic memory. It includes features such as deep copying, move semantics, concatenation, comparison, and stream operations, among others.

Detailed Description of the Custom String Class
This String class is a custom implementation of a string-like object in C++ designed to mimic the behavior of std::string while providing complete control over dynamic memory management. By manually handling memory allocation, copying, and deallocation, the class demonstrates key concepts of object-oriented programming, including encapsulation, operator overloading, deep copying, move semantics, and resource management (also known as RAII—Resource Acquisition Is Initialization). It offers a range of features that are often required for efficient string manipulation, including concatenation, comparison, and stream operations.

Below is an in-depth description of each aspect that this class covers.

Key Features and Capabilities


1. Dynamic Memory Management
The class allocates memory dynamically to store string content using the new operator.
Every instance manages its own memory, ensuring that different objects maintain independent copies of their strings (through deep copying).
Memory is released explicitly through the destructor to avoid memory leaks.
This fine-grained memory control teaches concepts such as manual resource allocation and deallocation, which are hidden in std::string.


3. Deep Copying
Deep copy constructors and assignment operators ensure that each string object maintains its own copy of the data, rather than sharing it with others.
This prevents issues such as dangling pointers or accidental modification of data in multiple objects referencing the same string.
Example:


String s1{"Hello"};
String s2 = s1;  // Deep copy - s2 is a separate object with its own memory


3. Move Semantics
Move constructors and move assignment operators efficiently transfer ownership of resources between objects without unnecessary copying.
This is essential for performance optimization, especially when dealing with large strings, as it avoids expensive memory operations.
Example:


String s1{"Hello"};
String s2 = std::move(s1);  // s1 is now empty, ownership transferred to s2
After the move, s1 is set to nullptr to prevent double deletions during destruction.


4. Operator Overloading
The class overloads multiple operators to provide intuitive usage and behavior similar to std::string.
Some of the key operators implemented include:

Concatenation Operator (+): Allows joining two strings to form a new one.
Comparison Operators (==, !=, <, >): Supports lexicographic comparisons of two strings.
Unary Operator (-): Converts a string to lowercase.
Multiplication Operator (*): Repeats a string multiple times.
Increment Operators (++ prefix and postfix): Converts all characters to uppercase.
Compound Addition (+=): Appends one string to another.
These overloaded operators enable natural and readable syntax, improving the usability of the class.

Example:


String s1{"Hello"};
String s2{" World"};
String s3 = s1 + s2;  // s3: "Hello World"


5. Stream Operations
The class overloads the input (>>) and output (<<) operators, allowing easy reading and printing of string objects through standard input and output streams.

Example:


String s;
std::cin >> s;  // Reads user input into the string object
std::cout << s;  // Prints the string to the console
These stream operators make the class integrate seamlessly with the C++ I/O system, just like std::string.


6. Self-Assignment Handling
Both the copy assignment and move assignment operators check for self-assignment, ensuring that an object is not accidentally assigned to itself.
This prevents unnecessary operations or resource leaks when such a scenario occurs.

Example:


String s1{"Hello"};
s1 = s1;  // Safe due to self-assignment check
7. Resource Management through RAII
The class follows the RAII (Resource Acquisition Is Initialization) principle, where resources are acquired and released within the object’s lifetime.


Memory is allocated when the object is created, and the destructor releases the memory when the object is destroyed.
This ensures exception safety and avoids memory leaks in case of unexpected program termination.
Example:


{
    String s{"Temporary String"};
}  // Destructor automatically releases the allocated memory here.


Performance Optimization through Move Semantics
Using move constructors and move assignment operators ensures better performance, particularly in cases where temporary objects are involved. By transferring ownership instead of copying, the class minimizes memory allocations and deallocations.

Example:


String func() {
    String temp{"Temporary"};
    return temp;  // Move semantics prevent an unnecessary copy here
}


Use Cases and Practical Applications
Building custom libraries: This class can serve as a foundation for building a more complex string library.
Learning memory management: It’s an excellent exercise for understanding manual memory handling in C++.
Operator overloading practice: Provides practice for implementing intuitive syntax through operator overloading.
Optimizing large text manipulations: With move semantics, it’s suitable for handling large text data efficiently.
