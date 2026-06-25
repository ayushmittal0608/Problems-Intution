We have already find out that how can we find the basic binary search, lowest occurence, highest occurence and mid occurence using binary search but what if array is rotated and then we need to find the element from the array.

In order to search the element in a rotated array, we need to look upon the two search spaces from low to mid and from mid+1 to high. Now, this part is used to find out that in which search space do we need to search the element, for eg, we have 4 5 6 7 1 2 3, now our arr[mid] is 7 and arr[low] is 4, so if arr[mid]>arr[low], we know where to find element, which is the first part from 4 to 7, now comes the target that we need to find, so between 4 to 7, if target lies, then we shift high=mid-1 while if it doesn't lie, then we shift low=mid+1. So, here, one is the orchestrator and other is the optimal finder and finally, we can find out that target element index inside an array.

```
int low=0, high=n-1;
while(low<=high){
  int mid=low+(high-low)/2;
  if(arr[mid]==target){
    return mid;
  }
  if(arr[mid]>=arr[low]){
    if(arr[mid]>target && arr[low]<=target){
      high=mid-1;
    }
    else {
      low=mid+1;
    }
  }
  else {
    if(arr[mid]<target && arr[high]>=target){
      low=mid+1;
    }
    else {
      high=mid-1;
    }
  }
}
```

Let's build an intution first, for eg, we have 4 5 6 7 1 2 3 and 7 is mid, so it comes between 4 and 7 and we want to search 5, so it comes between 4 and 7, so we have a search space from 4 as arr[low] to 6 as arr[mid-1]. If we want to search 2, so it comes between 1 and 3, so we know target is not between 4 and 7, so we have search space from 1 as arr[mid+1] and 3 as arr[high].

Now, second case is 5 6 7 1 2 3 4 and 1 is mid, so it comes between 1 and 4 and we want to search 3, so it comes between 1 and 4, so we have a search space from 2 as arr[mid+1] to 4 as arr[high]. If we want to search 6, so it comes between 5 and 7, so we have a search space from 5 as arr[low] and 7 as arr[mid-1].

So, whenever we think or assume this model of binary search in our mind, the mental model is to shift the search space to search the element and if it is sorted.

Now, more appropriate word to describe binary search is monotonicity because monotonicity flows in a single direction, either all increasing or all decreasing. Now, we all know how trapping rainwater is being implemented, let's say we just try to solve it using this search in a rotated array, maybe it could be solved. So, we know that there will be too much trapped rainwaters, so the idea is that it can be trapped between two walls, firstly decreasing and then increasing, so let's say we have a case 0 1 0 2 1 0 1 3 2 1 2 1, now to trap a water, we need a wall which is segregated into two parts, left and right between which we have many search spaces to find the trapped water, for eg, initially arr[low]=0 and arr[high]=1, now water can flow out, so we do left++ and get both as 1 and then we have a wall to protect and estimate in our local search space, so initially max at left is set to 1, so we have it as 0 water trapped, now we go to 0 which is less than 1 in right side but also less than left max, so 1 water trapped, now when it goes to 2, water flows out, also our global is 1 that we need to shift to 2, so max at right would become 2, now water from right side becomes 0, then 1 and then again 0, so now we have a trapped water of 2 and then finally, we reach 3, so now wall becomes 2 for left and 3 for right, now we also have max at left as 2, so we calculate it and finally get 4 as 2-2=0, 2-1=1, 2-0=2, and 2-1=1, so in total, we have 4 trapped water for such search space, this way we calculate the total trapped water as 6.

```
int low=0, high=n-1;
while(low<=high){
  if(a[low]<a[high]){
    if(a[low]>=leftMax){
      leftMax=a[low];
    }
    else{
      water+=leftMax-a[low];
    }
    low++;
  }
  else{
    if(a[high]>=rightMax){
      rightMax=a[high];
    }
    else{
      water+=rightMax-a[high];
    }
    high--;
}
cout<<water<<endl;
```

So, now this is how binary search is capable of handling monotonicity, here in this example, we are not having an optimal search space using mid element because it is not a rotated array or some case like that but we are manipulating the walls as per our requirement, by shifting low and high as per the requirements, so a mix of two pointers, greedy and binary search. We can think of search in a rotated sorted array as mid as some orchestrator and target search as optimal finder, while in case of trapping rainwater, it becomes somewhat a complex version of previous problem where we have left and right or low and high as some orchestrator and their max-currentHeight as the optimal finder to find all of the possibilities at the tip of hand.

This is really an interesting problem, trapping rainwater and I love solving this problem as it reflects the beauty of binary search, prefix sum, monotonic stacks, etc, but let's stick to binary search now and the way it is being solved reflects the beauty of binary search. So, now we can list it as some important pattern to solve many problems efficiently and effectively.























