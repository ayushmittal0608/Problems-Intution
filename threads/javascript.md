Let's discuss about threads because that crash course or skill acquiring syndrome also includes something where whenever we are so called learning some skill, we have an intution that we have mastered this skill, now we will apply to jobs resonating with this skillset and get a nice package. But if we go deep to a certain level, we might notice that learning or acquiring a skill is equivalent to learning a wrapper and it would be nice to be dumb rather than taking crash course or acquire skill through these wrappers.

So, if we need to understand threads, we need to know that we require threads to make full utilization of number of cores of the CPU processors. So, for eg, we are having a multi core CPU processor and we want to parellelly execute each of our task rather than being dependent on one task taking this much time, then next task and so on. So, for better utilization of our CPU cores, we divide the tasks into multiple threads in order to execute each task in parellel to other tasks, finally being synchronized through thread synchronization.

Now, in order to coordinate between different parts of some application, if multi-threading happens, then one thread being freezed doesn't affect other parts and hence, we can rapidly switch through time slicing so that all our options are being available to cancel the action or switch and so on. So, we really need threads.

But javascript is single threaded and we need to properly utilise the multiple cores of CPU, multiple threads to distribute our work effectively, so we make use of Node.js runtime environment built on V8 javascript engine written in C++. So, we make use of libuv thread pools where we have large number of worker threads which solves the single threaded problem of javascript, and offer us a large number of worker threads which can be useful in performing heavy computations parellelly and having full utilization of multiple cores of CPU.

Now, we need to know that where do we need to use worker threads, like for eg, if we utilize them for CRUD operations, then initializing worker threads creates an overhead that adds to the execution time, and takes much more time than normal CRUD, so obviously we need to change the approach and try to execute it for CPU based operations rather I/O based operations, because it involves heavy computations, so we need to allocate worker threads to perform heavy computations in order to prevent it to affect our main thread and is executing computations in parellel.

Now, this is how threads are being implemented and executed in Node.js since javascript is single threaded, so we need to wait for one operation to be executed, so as to get to the next operation.

And now if we want to scale our infrastructure more, the best thing is to switch to rabbitMQ and its message queue is the best thing and the way how it manages the failures to dead letter queues and its background job processing is exceptional. So, most of the time, even if we are building something B2C and it is the just the early stage but our vision is to scale it, then rabbitMQ is the best choice.






