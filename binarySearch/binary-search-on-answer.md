# Binary Search on Answer

Let's firstly understand this algorithm, binary search on answer, it means we have an answer which lies in a search space but it could only be obtained following certain criteria or condition, that it needs to reach atleast this much part in order to get the answer.

We know that binary search use to work in monotonic search space and let's assume we are having a condition where we need to split an array into k parts where we want all such parts in a way that maximum sum or largest sum is minimized. Let's say there are 6 people in an organization where we need to split those into 3 groups in such a way that every group is comparable to each other, which means we do have the high performing group but still we need to keep the competition balanced. I just hate this word competition though but sometimes it's a perfect example to illustrate this algorithm, but if I hate this word, it won't maintain the equilibrium, so let me balance the word competition by not hating it, making it comparable enough to solve this problem.

So, we have 1, 2, 3, 4, 5, 6 as an array and it depicts the amount of work every person can complete in say 1hr. So, if we have [1, 2, 3] as group 1 and [4, 5] as group 2 and [6] as group 3. Now, the competition is balanced and equilibrium is being maintained. Now, how can we solve it algorithmically.

Let's say what is the maximum amount of work all combined can do, so we will infer that it is equivalent to 21 and the highest value is 6, so we know that minimum in search space is what we can take as is 6. Now, we need to find the mid element in that search space which is 13, so it will be 1+2+3+4=10, so it will be great if k=2 but now we want 3 groups, so k hasn't yet reached to 3, so let's say we reduce the search space to 6 and 12 and then mid will be 9 and finally we have got the largest sum which is minimized.

So, it is implemented as:

```
bool canSplit(vector<int>& nums, int mid, int k){
  int count=1;
  int last=0;
  for(int num:nums){
    if(num+last<=mid){
      last+=num;
    }
    else{
      count++;
      last=num;
    }
  }
  return count<=k;
}

int main(){
  vector<int>nums={1, 2, 3, 4, 5, 6};
  int k=3;
  int low=*max_element(nums.begin(), nums.end());
  int high=accumulate(nums.begin(), nums.end(), 0);
  while(low<=high){
    int mid=low+(high-low)/2;
    if(canSplit(nums, mid, k)){
      ans=mid;
      high=mid-1;
    }
    else{
      low=mid+1;
    }
  }
}
```

Now, if the condition is to maximize the minimum sum, then how will we gonna implement it. For eg, we are currently having an array 1, 2, 3, 4, 5, 6 and we want to split it into k=3 groups, maximizing the minimum but also splitting them into 3 groups. So, firstly our search space needs to be designed in a way that could accommodate minimum of the values, so we take it from 1 to 21 and hence, we would have 11 as mid element and we will get total count of 1 as 1+2+3+4+5=15 that satisfies sum>=11, but we need a count of atleast 3. Now, we split further from 1 to 10 which comes out to be 5. Now, we have 1+2+3>=5, then 4+5>=5 and 6>=5. Now, here we have maximized from the starting to get the minimum sum at the last when count>=k.

```
bool canSplit(vector<int>& nums, int mid, int k){
  int count=1;
  int sum=0;
  for(int num:nums){
    sum+=num;
    if(sum>=mid){
      count++;
      sum=0;
    }
  }
  return count>=k;
}

int main(){
  vector<int>nums={1, 2, 3, 4, 5, 6};
  int k=3;
  int low=*min_element(nums.begin(), nums.end());
  int high=accumulate(nums.begin(), nums.end(), 0);
  while(low<=high){
    int mid=low+(high-low)/2;
    if(canSplit(nums, mid, k)){
      ans=mid;
      high=mid-1;
    }
    else{
      low=mid+1;
    }
  }
}
```

Now, why we have taken count>=k instead of count<=k. It is because of the reason that if by any chance, during search inside a search space, we get count>=k, then also we can return the last sum because it remains the same and the 4th split that happened would get merged with 1 or 2 because obviously, we want minimum sum to be maximized.

In case of minimizing the maximum sum, we get the maximum sum at later parts which is minimized, so in case, firstly, it is 2 splits and then 4 splits, so we want something like count<=k, so we need to split into 2 parts, now we can continue with 2 parts and the second part would obviously be the largest one while for first part, we will split it into 2 parts more and finally we can get largest sum.

I thought I would have this part unique with some better explanation so that we could enjoy the beauty of this algorithm that we use but it is being explained in a way that isn't showing any taste in the explanation. There were days where I had better thoughts and explanations regarding this algorithm but I was busy that time, but I think more the thoughts would come and be written and trying to be executed could broaden our mind to think about the different cases, possibilities and how can we approach to solve real world problems because knowledge of any algorithm is one thing while thinking about the problem which exists and not yet solved would be how we can grow as a person and I thought more practice of it could get us reach there.










