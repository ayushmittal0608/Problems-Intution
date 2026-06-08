In order to become good at C++, we first need to know what is really happening inside the iostream code that we uses generally like the cin and cout.

we generally use cin>>a; and cout<<a<<endl;

From where does it come from? We have two things: istream and ostream where istream is responsible for taking input stream from keyboard, files, etc. and ostream is responsible for taking output stream from keyboard, files, etc.

Input -> Processing -> Output

Now, whenever we write std::istream f("a.txt"); int x; then f>>x; we will take x as input inside a.txt file.

Similarly, whenever we write std::ostream f("a.txt"); f<<x; we will get x as output inside a.txt file.

Now, real work between istream and ostream is done by stream buffers.

The istream asks buffer for data and calls streambuf->sgetc() and now buffer checks internal memory, so it refills from OS where OS reads data from keyboard and read happens as read(fd, buffer, size) where fd determines the keyboard being used, buffer resembles the pointer to the memory block and size is the maximum size of that read, now this buffer is passed into stream buffer.

Hence, character goes into buffer and istream parses them to data type like int, float, etc. and it gets converted into the required data type.
What if there is something like AI sitting over the stream buffer and as OS reads data from keyboard, which is a prompt and renders the data as per the instructions from keyboard to AI, now AI would interpret the things and generate code relative to prompt buffer. Now, there is some processed value, for eg, I give a prompt that "You are the system driver and I want you to take input as ${`Ayush is a nice person`} and break this sentence into 4 words. Hint to do so is using stack data structure where at each space, you push the string inside the stack." Now, this data as a new buffer is passed to stream buffer for storing it to memory.

Then, next task is for ostream to write into buffer where we display stored data where buffer stores data temporarily and flush happens when buffer is full, forcing data to be displayed inside console screen and os writes a call write(fd, buffer, size) where fd is monitor id because we are displaying it over a monitor.

In the cpp file, mentioned above, wistream and wostream are taken for wide characters and that glibcxx_iostream is nothing but a macro is defined which ignores if iostream comes more than once in a code and hence it was a simple code.

So, in this readme, we have discovered how cpp I/O abstraction is layered. It would become more complicated if x86 and assembly programming comes but maybe we can try finding some way out so that we can have something which could directly convert high level language to machine coding, maybe if we think in terms of AI.
