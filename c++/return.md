Q. What is return?

This is the most important part in C++, maybe without it, we can't perform recursion, recursion is a big word to say, let's say it functions calling functions or calling stacks. Let's say we build a normal array int arr[n]; now this is having a stack memory and we are executing something inside this array, let's say fibonacci series of a[i]=a[i-1]+a[i-2]; starting from i=2 to n and taking a[0] and a[1] as 0 and 1.  Now, what happens is that we are having a single stack memory where we are executing the series, then once we get the whole array, we return its last element as an answer but then after that, we use return 0; we do it so that it exits the program memory and stack which is being used, nowadays its pre-installed in compilers to exit program memory. So, what just happens inside return is:

```
main:
  mov eax, 0
  ret
```

Now, let's say we have implemented a recursion, so it will be like if(n<2){ return n; } and then return fib(n-1)+fib(n-2); Now, in this we are calling stack one by one, for eg main stack -> stack fib(n) -> stack fib(n-1) -> stack fib(n-2) -> stack fib(n-3) and so on.

```
fib:
  // if(n<2)
  cmp rdi, 2 // rdi (destination address) is equivalent to n
  jl base_case // jumps to the base case where we return n;

  push rdi // pushes rdi to stack
  
  mov rdi, rdi // move n inside n
  dec rdi // then decrease n by 1 to make it n-1
  call fib // call fib(n-1)
  mov rbx, rax // now we have fib(n-1) stored inside temporary storage

  pop rdi // restore original n
  sub rdi, 2 // then decrease n by 2 to make it n-2
  call fib // call fib(n-2)

  // return fib(n-1)+fib(n-2)
  add rax, rbx // now add fib(n-1) stored as temp storage to rax
  ret // finally exit the program memory

base_case:
  // return n;
  mov rax, rdi // we move n to rax (accumulator)
  ret // exits program memory
```

Now, we are calling stacks again and again due to which OS becomes stack heavy while if we execute it all inside single memory stack, it would be much faster approach with improved latency and less overheads.

This is the reason why we need to avoid memoisation in DP and adopt tabulation as the best practice because everytime we need to store the dp[n] as cache when we utilise if(dp[n]!=-1){ return dp[n]; }. Now, we are storing and calling more and more stack and also storing this value in cache or temporary storage as rbx which can cause too many overheads.

Now, let's talk about DFS and why we don't face such scenario in DFS, it is because DFS do calls the stack again and again but it does it parellely like parellel to its neighbour, for eg, we have 

```
for(int neighbour:adj[n]){
  if(!visited[neighbour]){
   dfs(adj, neighbour);
  }
}
```

Now, in this approach, we are calling stack A -> then call stack B, then C and so on in a single depth, then we iterate it up in case of no new neighbour and again start calling like stack A -> then B1 -> then C1 and so on. So, there is a stack frame which maintains it calling much less or no overhead and no latency or performance issue due to which one can freely utilise both BFS and DFS for the process and both are having same complexity too.

In case of void functions, we just exits the program memory and stack and nothing is moved to rax because we don't return anything in it.

```
void:
  ret;
```











