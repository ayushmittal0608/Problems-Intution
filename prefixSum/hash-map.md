We are given an array and we need to count number of subarrays whose sum is equal to k, how will we calculate it?

## Concept Name: Hash Map + Prefix Sum

We take a hash map and initially take freq[0]=1 and then iterate over the whole loop increasing the prefixSum and keeping it inside freq[prefixSum], increasing it. Now, when we get prefixSum-k inside the freq, we increase the count to count+freq[prefixSum-k], but why have we taken freq[prefixSum] and increased it as we just have to take care of freq[0] to find. If we quietly observe it, we notice that we need to shift subarray as well while finding prefixSum-k.

```
freq[0]=1;
for(int i=0; i<n; i++){
    prefixSum+=a[i];
    if(freq.find(prefixSum-k)!=freq.end()){
        count+=freq[prefixSum-k];
    }
    freq[prefixSum]++;
}
```

So, what we have noticed so far is that for contiguous segments, prefix sum is the most optimal way for calculations, so wherever this concept of sliding window appears, we have variety of choices on what to opt and we can use sliding window using i from 0 to n and then j, but it is only relevant for positive numbers

- elite celebrity: Maybe in future, you don't have to use stacks, queues or sliding window

- podcaster: really??

- elite celebrity: Ya, because most of the stacks, queues or sliding window jobs would be replaced by prefix sum, even we are planning to replace all DP jobs as well with prefix sum and most of it have already been done.