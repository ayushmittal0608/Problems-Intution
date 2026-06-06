We are given an array and we need to find sum from l to r, how will we calculate it?

## Concept Name: Range Query Sum

P[i] = A[0] + A[1] + ... + A[i]
sum(l,r) = P[r] − P[l−1]

Now, there is some interesting concept which we use in our daily life where length of this subarray calculated is r-l+1 and we use it inside sliding window algorithm as well and many a times, inside stacks and queues.