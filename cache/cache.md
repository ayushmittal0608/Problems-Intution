Q. What is cache?

In layman language, cache is something which stores data temporarily to deliver it faster. Now, every person has their own definition of cache on the version they are working upon. Let's say there is a hardware engineer, he will talk about L1, L2 and L3 cache where CPU hits to load memory directly rather than calling registers for the same.

Now, if we talk to a cloud engineer, namely someone at AWS or azure or GCP or many more, they would talk about CDN cache which stores web assets and API responses closer to the user. It could be the work of a devops engineer too that how are someone managing web assets through CDN cache. This CDN cache takes us to many such dimensions where we derive the CAPs theorem and that would be an interesting part to focus upon because through CDN, we are not storing data at one availability zone but it is spread over multi-availability zones and what CAPs theorem generally depicts is the consistency, availability and partition tolerance.

Now, if we talk to a network engineer, they would take about DNS cache where during the DNS resolution, some IPs are being cached in the OS or browser so that they can be mapped easily with domain name.

Now, if we talk to some web engineer, they would talk about how some of the static web assets are being stored on their device, so that when they load previously visited webpages, they could easily be able to load them.

Now, if we talk to some full stack developer, they would talk about in-memory cache which stores computational data directly inside the application processes.

Similarly, if we talk to some database engineer, they would advice us to use cache to store data temporarily so that we need not have to retrieve it again and again even if they have used the best practices of indexing inside database, still they won't advice us to fetch data from DB directly as its computation cost is too heavy.

So, these are different layers of cache being used in system, for eg, I execute a C++ command and CPU assigns a virtual address to the assembly version CPU has executed, then MMU containing a page table maps these virtual addresses to the physical address at an offset, now finally CPU hits the cache to load data and if all miss, then data comes from RAM and is loaded into CPU registers for computation through ALU. Now, the L1 cache is the fastest as it stays near to the CPU and is having the smallest capacity, then comes L2 cache which is somewhat slower than L1, mid-capacity and L3 cache is the slowest among all, and highest capacity, also it lies near to the RAM, but still faster than RAM. So, the most effective cache hit for CPU is always the L1 cache but since we want a perfect balance of speed and capacity, L2 cache is the most balanced preference.

Now, let's discuss about the browser cache which has an in-memory cache which we generally resolve using hard refresh (Ctrl+Shift+R) and it is stored in the memory of browser temporarily, but there is another cache too that lies inside the disk of our device at location
"C:\Users\AyushMittal\AppData\Local\Google\Chrome\User Data\Default\Cache" which chrome saves inside our disk, which are images, js, css and other static contents and it uses LRU cache for it.

This is the beauty of cache that it enhances our experience while using any system, either it is hardware or software or database or anything.

## Cache Eviction
For eg, our cache memory fills up and our cache data is unable to hold more data, so it removes the data from the back and add the data to the front. Now, there are two types of cache eviction policies that we generally use, one is based upon LRU being evicted and other where LFU is being evicted. Now, we have large number of use cases of it in different domains and that is the art on how we use it inside the systems. There are other types of eviction policies: LRU, LFU, MRU, Random Eviction, etc.

## Cache Stampede
For eg, we have loaded a large amount of data and eventually, our cache stops working or is not taking that load to hold and cache data, then the whole load is directed towards the database making the server going down and increasing the overall downtime.

Now, let's understand about how it derives CAP theorem. CAP theorem states that data store can simultaneously provide atmost of two guarantees: CA, AP or CP. Now, if we are talking about cache, then obviously we can't believe that all of the three are guaranteed at the same time, however in other cases where network failure and other parameters go right, we can achieve it, but when we talk about cache, then let's say we have two nodes, A and B, so we are handling partition tolerance at the time of network failure, now two conditions arrive when both of nodes see same data, ensuring consistency. Now, to ensure consistency, when we update A, then A can't synchronise with B, leading to the write at A becoming down and we mark that service unavailable due to non-synchronisation. Now, if we prefer availability, then we would have inconsistent data to serve through different nodes. So, in case of cache, we prefer to use stale data rather than consistency, for eg, we have old data displayed through cache rather than new data from DB which prefers AP over CP, and this is the reason, web engineers actually face the issue of too much cache causing old and stale data to appear rather than upgrade due to inconsistency and high availability.
