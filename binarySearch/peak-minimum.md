Now, for eg, we are given an array either sorted or rotated sorted array and we need to find minimum element inside it that what could be the minimum element in that array? Let's say we have an array as 4, 5, 6, 7, 0, 1, 2 where we know 0 is the minimum element in the array but how would we find it? Let's say we need to find 0 and we don't have anything but just low, high and mid element which are 4, 7 and 2, now we need to slide using mid in such a search space that we can easily find the minimum element, so if arr[mid]>arr[high], obviously we shift low to mid+1 to slide our search space, but if arr[mid]<=arr[high], then high=mid because we want a search space between 4 and 7 and finally, we will get minimum element in an array. Now, one thing we need to keep in mind is that it should be low<high not equal because if say we have at 0th position both low and high, then high will again and again become 0 and get stuck in a loop

```
int low=0, high=n-1;
while(low<high){
  int mid=low+(high-low)/2;
  if(a[mid]>a[high]){
    low=mid+1;
  }
  else {
    high=mid;
  }
}
return a[low];
```

Now, let's say we need to find the peak element in an array, which is we know that it is 7, but if after mid, there exists some mid+1 which is greater than mid, so need to move low to mid+1, why so because mid+1 element>mid element and we obviously remove the whole search space from low to mid because obviously that is not the peak and it needs to be eliminated, so now search space becomes from mid+1 to high, now to find the peak one, we either shift again to next mid+1 or if there exists mid element>=mid+1 element, then we shift search space further by making head=mid, now mid+1 is already the peak, and at next position, we are going just down, so obviously we shift high to mid to squeeze our search space more and we will finally get the peak value.

```
int low=0, high=n-1;
while(low<high){
  int mid=low+(high-low)/2;
  if(a[mid]<a[mid+1]){
    low=mid+1;
  }
  else{
    high=mid;
  }
}
return a[low];
```

In order to solve any binary search problem, we need to first check monotonicity and if it exists, we take mid value and use mid as an orchestrator to slide search space and finding out the solution based on comparison. So, it becomes a pattern and new problems arise due to the mental upgradation. Now, if this becomes the pattern in our reflexes, we can solve many problems using it, now that new problems are building some algorithm or some mental model which when we practice becomes a pattern in our reflexes to solve more and it tends to infinity, now the mental model can solve many problems but if it is genuinely used in a system, it becomes an evolution parellelly otherwise we can solve n number of leetcode or codeforces problem, we are not fetching any ROI from it.










