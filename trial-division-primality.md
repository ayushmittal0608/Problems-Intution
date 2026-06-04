Now, we need to check whether n is prime or not, how will we calculate it?

## Concept Name: Primary Check(O(root n))

if we notice the pattern, then if we start from 5, then 5 and 7 are the numbers which are prime and n can be divisible by them, then next comes after +6 which is 11 and 13, then +6, which is 17 and 19 and so on.

So, we take n%i and n%(i+2) and find whether it is prime or not, whether it doesn't give zero or not. If it returns 0, then obviously it is not a prime.

Base condition will be n<=3, then return true and since 1 and 0 are not prime, we return false and if it is divisible by 2 or 3 and return 0, then also return false.
