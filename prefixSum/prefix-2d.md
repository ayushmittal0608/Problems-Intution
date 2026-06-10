Now, we have seen that how can we calculate prefix sum of 1d array but what if array is 2d because it might happen that we have a grid where we want to perform operations and have to maintain that contiguous segment or a block that what is the sum that comes, so in order to build it, we need to play an interesting activity where we initially are at arr[i][j] and for finding sum, we take (i-1, j), and (i, j-1) and add the sum calculated at those parts to pref[i][j], also subtract the (i-1, j-1) part from it, just visualise the set and you will get the answer and form prefix sum 2d array using it, so first remains the same, the next one will have (i+1, j) and then (i, j+1) where we use pref[i][j] going to those places, just perform that fun activity and get the result out of it, so now we will get to know that we have a function:

  $$ pref[i][j]=arr[i][j]+pref[i-1][j]+pref[i][j-1]-pref[i-1][j-1]; $$

Now, for calculation of difference or adding any value or sum to any of the prefix array, for eg, (i1, j1) to (i2, j2), we find add to pref[i2][j2] and pref[i1-1][j1-1] and subtract from pref[i1-1][j2] and pref[i2][j1-1], let's visualise it like arr[i][j] is made up of pref[i-1][j], pref[i][j-1] and pref[i-1][j-1], now we have arr[i][j] and pref[i-1][j-1] which is all we need for that block but arr[i][j] have elements of pref[i-1][j] and pref[i][j-1], which we need to remove and add pref[i-1][j-1] because then it will remove that part of block too. So, we need not have to remember it, just it comes through intution.

$$ sum of block=pref[i2][j2]+pref[i1-1][j1-1]-pref[i1-1][j2]-pref[i1][j2-1]; $$

Now, what if we have to find some category like it is 0, 1 or 2, or count of vowel or count of prime, now how will we do it? Let's see it in next readme.
