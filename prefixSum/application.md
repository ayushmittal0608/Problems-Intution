Now, the application for prefix count can be count of vowel, 0,1,2 or prime numbers. Now, how would we solve it using prefix sum where we have an array and we need to calculate the count of 0, 1 or 2 or prime numbers in it or vowels in it.

For 0, 1 and 2, we increase prefix sum count at different categories where category is taken like for eg, arr[i]=0 or 1 or 2, then we take pref[i][cat]=pref[i-1][cat] and then increase pref[i][cat]++; now we can find the count of that category at each point, now not only for all but we can calculate for contiguous block too like from i to j or if it is a 2d grid, it becomes 3d, now this is not only 0,1 or 2, it can be anything like any fruit, vegetable, country, etc.

If we talk about vowel or prime numbers, we have a whole list from where we need to check if it is a vowel and if so then we place inside the prefix sum and increase its count and same for prime numbers and anything related to checking.

Let's say we have n tasks where some are pending, some are failed and some are success, so these becomes categories and for each category, we find it, now we want to check tasks from i to j, so we can view them. Let's say these status are not given in array and we need to check status, the catch is that the nth or 1st letter of the username shows the address and username is inside the array, so we check success status against the 1st letter or nth letter like a[0] or a[n-1] === 'S', so now it filters all the S and display from i to j.

This way we can solve any problem through critical thinking, just forget sliding window, fixed window, two pointer, three pointer, n pointer, etc. just try to get through the beauty of these algorithms that they can build the most efficient systems for us.
