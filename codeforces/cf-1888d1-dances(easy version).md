This is the easy version of the problem. The only difference is that in this version m=1.

You are given two arrays of integers a1,a2,…,an and b1,b2,…,bn. Before applying any operations, you can reorder the elements of each array as you wish. Then, in one operation, you will perform both of the following actions, if the arrays are not empty:

Choose any element from array a and remove it (all remaining elements are shifted to a new array a),
Choose any element from array b and remove it (all remaining elements are shifted to a new array b).
Let k be the final size of both arrays. You need to find the minimum number of operations required to satisfy ai<bi for all 1≤i≤k.

This problem was too easy, so the problem author decided to make it more challenging. You are also given a positive integer m. Now, you need to find the sum of answers to the problem for m pairs of arrays (c[i],b), where 1≤i≤m. Array c[i] is obtained from a as follows:
c[i]1=i, 
c[i]j=aj, for 2≤j≤n.

Input
Each test consists of multiple test cases. The first line contains a single integer t (1≤t≤104) - the number of sets of input data. This is followed by their description.
The first line of each test case contains two integers n and m (2≤n≤105, m=1) - the size of arrays a and b and the constraints on the value of element a1.
The second line of each test case contains n−1 integers a2,…,an (1≤ai≤109).
The third line of each test case contains n integers b1,b2,…,bn (1≤bi≤109).
It is guaranteed that the sum of nover all test cases does not exceed 105.

Output
For each test case, output the total number of minimum operations for all pairs of arrays (ci,b).

Intution: It's a super easy problem, we just need two pointers i and when we observe m, then we realise that arr[0] is the only element that varies from 1 to m, so it could be either 1 at lowest or m, so we take m as threshold and so we put arr[0]=m. Now, we know the answer, we will run binary search, increasing both if a[j]<b[i] and if not we increase i so that b would have some other element to compare with i and then we again increase i and j, this way we will easily get the answer consisting of how many pairs satify the situation.

Approach: Same as intution

Time Complexity: O(n log n)

Code:
```bash
#include <bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n, m;
        cin>>n>>m;
        vector<long long>arr1(n), arr2(n);
        arr1[0]=m;
        for(int i=1; i<n; i++){
            cin>>arr1[i];
        }
        for(int j=0; j<n; j++){
            cin>>arr2[j];
        }
        long long i=0, j=0;
        sort(arr1.begin(), arr1.end());
        sort(arr2.begin(), arr2.end());
        int ans=0;
        while(i<n){
            if(arr1[j]<arr2[i]){
                i++;
                j++;
            }
            else{
                while(i<n && arr1[j]>=arr2[i]){
                    ans++;
                    i++;
                }
                j++;
                i++;
            }
        }
        cout<<ans<<endl;
    }
}

