We are given a value of n and we have to calculate co-primes upto n. How will we calculate it?

## Concept Name: Euler's Totient Function

If normally, we need to calculate it, we will find too many GCDs and then factors and then compute it, due to which it becomes too slow and even complicated, so the simple way of finding it is using euler's totient function.

p=n*(1-1/p1)*(1-1/p2)... and so on.

Now, from i=2 to i*i<=n, if n%i==0, then until it doesn't become anything else except the 0, we reduce it to n/=i and then for result, we find result-=result/i, this way, we will be able to get the result and what is result, the number of co-primes values upto n.
