Now, the next part comes is pref-suff which is the really important part and the real beauty of prefix sum. Let's say we find the max pref value at each phase in going from left to right and similarly, the max suff value at each phase is going from right to left. So, what is the need for calculating such things like from left to right and right to left and we are maximising the value at each phase. If we notice closely and visualise it, we notice that it is building a wall where we have a small wall, then comes much small wall but maximum will be prev wall and then it finds a much bigger wall, so in third phase, maxm will be third much bigger wall and this way we construct much bigger wall at each phase till the last, similarly from right to left too, this wall is being built and maximised.

Now, we have built the walls but let's say in suff at last, we have a maximum sized wall, which goes all along the way, so we will minimise the wall, so that we can contain the things within and once we construct that house, we realise that we have small walls or traps in between which are trapping water, hence we subtract them from the minimum.

This is how we can easily get a trapped rainwater and what other application can we have for it, maybe something trapped, maybe we are jumping to a lesser height but not more height than maximum height, so we are contained in that boundary, this same question appears as many times in many contests and the variation that it has is the real beauty of prefix sum.

The other question that comes is product of array except self where we calculate the product from left to right and right to left but to exclude that self part, we take 1 at 0 as well as n-1 otherwise it will become total_product*arr[i].

Now, comes the maximum absolute diff split, where we need to maximise the difference when we make a split, so let's say we make a split at some point i, so from 0 to i, if we have taken everything minimum, then we need to take maximum from i+1 to n-1 in order to get maximum diff split and if we have taken from 0 to i as maximum, then we need to take minimum from i+1 to n-1 in order to get maximum diff split and this way we will get maximum  absolute diff split as answer by maximising both with answer.

Now, this maximum absolute diff split is a classic CP trick which is used in too many contests as well. The beauty of this trick is to find maximum absolute diff split which might seem unobvious or unpredictable at first, but is the most powerful trick ever.


