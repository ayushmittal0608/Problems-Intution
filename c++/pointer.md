Q. What is a pointer?

Pointer is something which usually we get confused with and it is because we haven't perfectly understand it. What mistakes we do while understanding pointers is that we think int* is not a data type while int is a data type and *var is what is storing address in it, but when we realise it as wrong, we finally get to the essence of pointers that data type is int*, not int. Once we understand it, we have conquered the whole concept of pointer, now we know &arr[0] is an address which is stored inside var have an address data type which is int* and when we write var, it is an address, when we write &arr[0], obviously it is an address and if we write arr[0], then obviously it is not a pointer and to extract value from address, we dereference it as *var which is value arr[0].

Now, pointers are basically used for just passing the address of any data rather than copying and sharing data which is a complex process, however we have some smart pointers like unique_ptr for such things and the greatest privilege is that it deletes the rest memory once the function or process is being executed, optimising memory leaks and making process more efficient. But the problem is that our code needs to interact directly with hardware, OS, memory and even matches the CPU registers which is why we use pointers. Also, pointers are heavily being used inside the data structures like linked list, heap, tree, graph, etc. Whenever we are using dynamic memory, then all of our data stores inside a heap and pointer to all the heap data is being stored inside the stack.

For eg, int* ayush = new int[5]; now here ayush is a pointer stored inside stack and a heap-based contiguous memory block is created having length 5 which initially contains garbage value.

Now, comes the types of pointer:

1. Double Pointer: We store the address of pointer using double pointer and data type which is used is int** and for dereferencing it to get pointer, we use * and for getting original value, we use ** inside it.

2. Function Pointer: In this pointer type, we declare a function pointer for a function, we are using, for eg, int swap(int a, int b), we will use int ptr=(*ptr)(int, int) which is initialisation of a pointer, then we assign the address of function pointer as swap and then we return either ptr(10, 5) or (*ptr)(10, 5) which gives us the final result.

3. Smart Pointers: There are three types of smart pointers where unique pointer is used for providing exlusive ownership to a pointer, shared pointer is used to allow multiple resources to access exactly same resource, however it could lead to circular dependency sometimes where weak pointer is used to check whether temporary shared data becomes 0 and it uses weak.lock() for it, so when temp shared data goes out of scope, it marks the object dead to prevent memory leaks due to any sort of circular dependencies.

4. Dangling Pointer: Such type of pointers are those that still stores the memory address of blocks that has been deleted, deallocated or set free. Now, this giving back of such memory address back to OS can result in various bugs, security vulnerabilities and application crashes.

5. Virtual Pointer: Such type of pointers are being used before the functions, for eg we are maintaining a class of animals where we have dog, bird and whale as functions, now all these functions belong to animal, so we use virtual pointer before functions to connect animal class to dog, bird and whale function where animal class is storing these addresses or pointers, now we add a derived class over base class named as terrestrial, then that points to the dog and bird, then we add another derived class over this derived class as aerial, then that points to the bird and this way we build a virtual pointer for the class.

These are the pointers which are being used inside C++ which are the most important aspect to optimise memory leaks, improve latency and minimise overheads. Now, next important topic will be templates because they are widely used in every aspect, in maths, physics, electronics and so on.

