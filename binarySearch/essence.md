Q. What is a binary search algorithm?

The beauty of binary search is that when someone says that they have become the god of DSA, then binary search comes to humble them up. Another beauty of it is that it optimises the algorithm to a large extent, like we are getting O(log n) complexity and it is used in many other algorithms too like in trees, whenever we are constructing root->left and root->right, we dissociate them into two halves which is a perfect use case for binary search. But for that, we need to understand binary search deeply, like where it is used, because we might think that it is being used to search elements in an array, but when we realise that we are having a search space and there, we need to divide the search space based on the requirements given to us, we generally prefer to use binary search.

For eg, We have given someone a large ground and we also give him n number of days to finish the work, now he wants to optimally organise his n days for that work, and he is having a set of work that he have to do as a set or an array, then he can utilise binary search to get maximum output each day to complete work in n given days. For eg, now AI is coming to eat up my job and then I go to farms for farming and have set of work to do inside farms in n days which I have to organise efficiently, so I open my laptop and would implement the binary search.

Now, we know that simple template memory to understand binary search is a simple structure:

```
int low=0, high=n-1;
while(low<=high){
    int mid=low+(high-low)/2;
    if(arr[mid]==target){
        return mid;
    }
    else if(arr[mid]>target){
        high=mid-1;
    }
    else{
        mid=low+1;
    }
}
```

Now, the first basic that we need to understand to move forward in the journey of binary search is low, mid and high, for eg, in [1, 2, 3, 3, 3, 4, 5], we are having 3 as low occurence, 4 as mid and 5 as high occurence. As we know that binary search is being implemented just to humble people, so it has a long history in humbling not people but everyone and everything, for eg, mid, you are going too high, let me humble you, and similarly, it uplifts too like mid, you are getting too low, let me uplift you, also many a times, it balances mid too.

So, for finding it out, we need to think that how can the searching be done for getting such occurences, all we have is mid, low+1 and high-1, we know that since mid is going too high than target, it humbles the mid and even if it high reaches the target, we get mid, but it humbles high more to get first occurence, so it is like do you want to find first occurence, be more humble, more, more and more high-1.

Now, for finding the highest occurence, mid is going too lower than target, so we uplifts low to go more forward and forward and forward by storing mid as answer but still moving more forward through low+1, this way we can easily be able to find last occurence, uplift yourself more to move more forward.

Finding mid occurence, is a basic single template that we generally use as a base for memory muscle establishment in binary search to solve more problems and here, the mid has attained a bliss of being balanced, so we need to become mid occurence based mid to make our life better, so that we have everything to gain and nothing to lose, nothing to gain and everything to lose.