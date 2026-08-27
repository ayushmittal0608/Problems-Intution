CUDA (Compute Unified Device Architecture)

Whenever we are running some code, we used to implement multi threading utilizing the cores of CPU but still we need GPUs. We generally say that GPUs are multi-core processors and it is the main reason why GPU has the utmost importance. We can't call GPUs as something more powerful than CPU because still heavy computation needs the usage of powerful CPU cores but still each GPU core is smartly handling when given one task to perform and that is the reason why GPU is highly preferred.

So, GPU consists of too many SMs (Streaming Microprocessors) containing blocks and these blocks contains large number of warps, each containing 32 threads. So, this whole configuration is inside a grid, so a grid can be 1d, 2d or 3d or based on kernel we have chosen. Now, inside that grid, we have plenty of blocks and each block contains too many threads inside the warps. In order to calculate, where the particular thread is being located, we need to make use of a formula that is simple and we can derive it too, because let's say it is a 1d grid, and we have a block 3, so its block index is 4 if we start from 0, and each block let's say contains 8 threads, so it becomes its dimension of 8 blocks and we need to find out the thread 3 which is at thread index 4, so our formula becomes blockIdx * blockDim + threadIdx.

Now, why is there a need for such grids, blocks, warps and threads. What would we get out of it? Let's say if we don't have the configuration designed this way, we won't be effectively utilizing our threads for the computation. Now, this is the way how parellel computation could take place and we would be able to display pixels over the screen.

Such grids orchestration is what we used to do inside the DP algorithm as well, where we are initially having some matrix and we need to multiply two or more matrices which we call as matrix multiplication, where the base idea is to effectively utilize the performance of GPU for parellel computation. Let's say we are sending two of the parameters, one is the first matrix and second is the end matrix, now between these two matrices, we have k number of matrices and we need to find the multiplication in a way that we multiply matrix at i, k and j where i is first matrix, j is last matrix, and k is the mid matrix from i+1 to j-1, thereby making a split at (i, k) and (k, j) to compute further in order to calculate final minimum count. This could lead to a large number of possibilities parellelly to what is needed.

Now, for eg, I want to make an efficient minimum count algorithm in this matrix multiplication, if I utilize the function parellelly, then obviously my computation will be faster and more robust. When we get to the idea of how efficient this parellel computation technique is, we could easily be able to know the essence and requirement of partition DP concept where we do execute matrix multiplication, while computing the functions parellelly to each other.

The software engineering doesn't teach us to grab the course or learn something to get a nice job, but it teaches us how efficient and reliable system we can design, how one can optimize the code, reduce the cost of business, working in an unambiguous environment, unclear requirements, being a better problem solver and thinking in terms of making the system highly efficient with high performance computing, while also maintaining data integrity, and ACID properties, using best indexing, sharding techniques, managing disaster recovery and implementation of CDN to deliver at shortest path using djikstra or bellmann ford algorithm. The usage of rabbit MQ based message queues for better latency, idempotency and scalable architecture. This way we could be able to make the systems more efficient and reliable.













