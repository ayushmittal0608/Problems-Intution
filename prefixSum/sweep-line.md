Q. What is sweep line algorithm and why is it used in prefix sum?

Let's say we are given intervals from start to end, and revenue is given to us alongwith start and end intervals. This whole thing inside a 2d array. It means we have (start, end, revenue) and we want to calculate revenue at particular time period and we are given not one interval but number of intervals like from [(1, 2, 10), (2, 3, 20), (1, 5, 40)], and n=5 let's say, now we know that we have revenue 10 at 1, 10 at 2, then +20 at 2 and 20 at 3, similarly from 1 to 5, we have +40.

It would take n^2 complexity if we traverse each interval and then find on that particular interval, the sum but to optimise this approach, we take a vector and insert value at v[i-1] and remove it at v[i], why is it so? Because we have to nullify it while calculating the prefix sum value, so that we could get actually get the value in that interval. Let's say v[0] becomes 10, then v[1] comes where we get prev 10 value while calculating prefix sum, then v[2] comes where we notice that we need to nullify that 10 to get that interval, so we do v[i]-=10, so when we calculate prefix sum, we get 0 at that interval and we do it for each interval.

This way, we will get the value at all points, so for particular time period, we can find out the revenue, or from r-l+1 too, we can find it, like within that interval, this way we can get n number of parameters from this sweep line approach and prefix sum usage.

```
for(auto& q:queries){
  v[q[0]-1]+=q[2];
  v[q[1]]-=q[2];
}
for(int i=1; i<n; i++){
  v[i]+=v[i-1];
}
```
