Q. What is Namespace?

Namespace is a container that groups identifiers to avoid name conflicts. Now, what actually happens is that whenever we are using namespace and our compiler compiles the code, it mangles the name. The process known as name mangling is done to rewrite function or variable name to include extra info like for eg, let's take a namespace ayush.

```
namespace ayush {
  void print(int x);
}
```

Now, after mangling, we get a symbol containing all info about it like _ZN5ayush5printEi where _Z is a marker for mangled name, N is a nested name, 5ayush is length+name, 5 print is length+func_name and E means end of the name scope marker and i is integer, let's say we have char c, then we will have _ZN5ayush5printEc.

Now, there are some citations which are based upon namespace usage due to which we consider using namespace std; bad to use because let's say, we are having a code like:

```
#include<iostream>
#include<algorithm>
using namespace std;
int a=3;
int main(){
  cout<<a<<endl;
}
```

Now problem that occurs is that what if inside algorithm, there is something as std::a? It might cause an error due to conflict. So, whenever we use namespace, we generally don't declare it globally, we try to implement it inside block as using std::cout or just std::cout and so on. That's why the best practice is to use either std::cout or using std::cout; and it applies to every std like cin, string, etc.

Now, namespace isn't just used for std, it is also used for other namespaces like custom one too, for eg, we have built a namespace ayush, so we can have ayush::print(23); and this will execute 23. So namespace work at compiler level when converted to object file containing mangled name directives with symbols which are resolved inside linker, then final binary is loaded into OS and then CPU executes the machine code.



