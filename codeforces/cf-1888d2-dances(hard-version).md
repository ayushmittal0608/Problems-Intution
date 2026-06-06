This is the hard version of the problem. The only difference is that in this version m≤109.

You are given two arrays of integers a1,a2,…,an and b1,b2,…,bn. Before applying any operations, you can reorder the elements of each array as you wish. Then, in one operation, you will perform both of the following actions, if the arrays are not empty:

Choose any element from array a and remove it (all remaining elements are shifted to a new array a),
Choose any element from array b and remove it (all remaining elements are shifted to a new array b).

Let k be the final size of both arrays. You need to find the minimum number of operations required to satisfy ai<bi for all 1≤i≤k.

This problem was too easy, so the problem author decided to make it more challenging. You are also given a positive integer m. Now, you need to find the sum of answers to the problem for m pairs of arrays (c[i],b), where 1≤i≤m. Array c[i] is obtained from a as follows:

c[i]1=i,
c[i]j=aj, for 2≤j≤n.

Input
Each test consists of multiple test cases. The first line contains a single integer t (1≤t≤104) - the number of sets of input data. This is followed by their description. The first line of each test case contains two integers n and m (2≤n≤105, 1≤m≤109) - the size of arrays a and b and the constraints on the value of element a1. The second line of each test case contains n−1 integers a2,…,an (1≤ai≤109). The third line of each test case contains n integers b1,b2,…,bn (1≤bi≤109).

It is guaranteed that the sum of n over all test cases does not exceed 105.

Output
For each test case, output the total number of minimum operations for all pairs of arrays (ci,b).

Intution:
Similar problem that usually comes in an interview, just this one is slightly moulded, there we are having a huge problem due to constraint as we are taking m<10^9. Now, we can't just simply take arr[0]=m, we just have to take it till 10^9 but it will be highly inefficient, so our upper limit will be m and we will calculate from 0 to n-1. Since we are doing so, we will be having two snippets resembling upper half and lower half in binary search, we break them into X(lower) and m-X(upper). Now, these operations are happening on ans and ans+1, so total sum of operations performed with ans=(X)*(ans)+(m-X)*(ans+1).

Approach:
Same as D1, the only difference is m pairs of array because in previous one, we were having only a single pair of array, easy to compute but here it has gone to 10^9 like it should be less than that. Now, we will implement binary search on it and divide it into two halves for number of operations computation.

Code:
```bash
#include <bits/stdc++.h>
using namespace std;

long long findAnswer(vector<long long> a, vector<long long> b, int n){
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());
    long long i=0, j=0;
    long long ans=0;
    while(i<n){
        if(a[j]<b[i]){
            i++;
            j++;
        }
        else {
            while(i<n && a[j]>=b[i]){
                ans++;
                i++;
            }
            i++;
            j++;
        }
    }
    return ans;
}

int main(){
    int t;
    cin>>t;
    while(t--){
        long long n, m;
        cin>>n>>m;
        vector<long long>a(n), b(n);
        a[0]=1;
        for(int i=1; i<n; i++){
            cin>>a[i];
        }
        for(int i=0; i<n; i++){
            cin>>b[i];
        }
        long long curr=findAnswer(a, b, n);
        long long low=1, high=m, ans=1;
        while(low<=high){
            int mid=low+(high-low)/2;
            a[0]=mid;
            if(findAnswer(a, b, n)==curr){
                low=mid+1;
                ans=mid;
            }
            else{
                high=mid-1;
            }
        }
        ans=curr*m+(m-ans);
        cout<<ans<<endl;
    }
}

