Now, we are given two sorted arrays and we need to find the median of two sorted arrays, where we are given two arrays, a=[1, 3, 8, 9] and b=[7, 11, 18, 19, 21, 25], in this problem, we take an assumption of 4 values that either the two of the values belong to array 1 or both belong to array 2 or one from array 1 and other from array 2, so for array1, we take left1 and right1 but we know that on left side, whichever the value will be, should be maximum, afterall it has to pass all smaller values to reach there but on right side, we would take minimum value because maybe it would be greater than maxleft1 but still at the search space after that position, it should be minimum and same is the case for 2nd array, so we have maxleft1, minright1 and  maxleft2, minright2. Once we know it, we get to know what to return, now there will be two cases, if it is even, we return (max(maxleft1, maxleft2)+min(minright1, minright2))//2 and if it is odd, we return max(maxleft1, maxleft2).

Now, explicitly, two pointers is being used in this approach in an indirect way that we even can't notice and this is the real beauty of this problem. Now, we need an array that consist of both, 1st array and 2nd array, so we need to decide search space for this problem, hence part1=(left+right)/2 and part2=(len1+len2+1)/2 - part1, where left=0, right=len1 and len1 is length of array 1 and len2 is length of array 2. This way currently, we get the mid of 1st array and mid of 2nd array where our maxleft1 becomes part1-1 if part1 is not 0, else it becomes INT_MIN because we need to maximise it and same for 2nd array. Now, minright1 becomes part1 if part1 is less than len1 while if it becomes equal to len1, it goes out of the array, so we take minright1 as INT_MAX because we need to minimise it.

Now, we have maxleft1, minright1, maxleft2 and maxright2. Now, we know that we need to maximise the maxleft1 and maxleft2 but they should still be less than minright2 and minright1, obviously maxleft1<=minright1 because they lie in same array, so we need to check with respect to minright2 and same for the maxleft2, if so, then we finally get the answer but if maxleft1>minright2, we need to go back to right=part1-1 and if maxleft2>minright1, then we need to go to left=part1+1, so that we have some element to satisfy our search space conditions.

```
int left=0, right=len1;
while(left<=right){
  int part1=(left+right)/2;
  int part2=(len1+len2+1)/2 - part1;
  int maxLeft1=(part1==0)?INT_MIN:nums1[part1-1];
  int minRight1=(part1==len1)?INT_MAX:nums1[part1];
  int maxLeft2=(part2==0)?INT_MIN:nums2[part2-1];
  int minRight2=(part2==len2)?INT_MAX:nums2[part2];
  if(maxLeft1<=minRight2 && maxLeft2<=minRight1){
    if((len1+len2)%2==0){
      return (max(maxLeft1, maxLeft2)+min(minRight1, minRight2))/2.0;
    }
    else{
      return max(maxLeft1, maxLeft2);
    }
  }
  else if(maxLeft1>minRight2){
     right=part1-1;
  }
  else{
    left=part1+1;
  }
}
return 0.0;
```

Now, in this problem, there are two main things happening, either the search space extends or squeezes to give the solution, because we know that what are the conditions for elements to reach the final median, so now if we have maxleft1 and minright2, we check the greatest one, if satisfying condition, it is fine but if not, then we need to orchestrate it like if maxleft1>minright2, we obviously need to shift the right to part1-1 because we want maxleft1 to be smaller and the array is sorted in ascending order, while if maxleft2>minright1, then we need a higher minright1 to have element bigger than minright1 to be greater than maxleft2. Now, we have taken part1 and part2 as the mid of two arrays but in part2, the shift is mainly governed by part1 so that if we shift part1 side to right, part2 side will shift automatically to left side, so that both search space shrinks. Now, if we shift part1 side to left, then part2 side will shift automatically to right side, so that both search space extends.

Here, we find two elements in an array which exists in such a way that they are lesser than minright1 and minright2, which are being maximised locally in the array until they are not touching minright1 and minright2, while also finding minright1 and minright2 greater than both maxleft1 and maxleft2 but minimised locally in an array until they are not touching maxleft1 and maxleft2. Once, this mental model is clear, this problem can be solved with a lightening fast speed.










