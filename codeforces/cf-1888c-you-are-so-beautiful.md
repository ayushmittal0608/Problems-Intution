You are given an array of integers a1,a2,…,an. Calculate the number of subarrays of this array 1≤l≤r≤n, such that:
The array b=[al,al+1,…,ar] occurs in the array a as a subsequence exactly once. In other words, there is exactly one way to select a set of indices 1≤i1<i2<…<ir−l+1≤n, such that bj=aij for all 1≤j≤r−l+1.

Input
Each test consists of multiple test cases. The first line contains a single integer t (1≤t≤104) — the number of test cases. This is followed by their description.
The first line of each test case contains an integer n (1≤n≤105) — the size of the array a.
The second line of each test case contains n integers a1,a2,…,an (1≤ai≤109).
It is guaranteed that the sum of n over all test cases does not exceed 2⋅105.

Output
For each test case, output the number of suitable subarrays.

Intution:
It looks dangerous but it is a simple problem, we firstly need to build subarrays, so firstly we identify the subarrays like for eg, 2 3 2 1 is a case where 2 has come twice, so we start with first 2 and we get 23, 232, 2321 and then we go to 3 and we get 3, 32, 321 and then we have already visited 2, so we jump to 1 and we get 7 as final answer. We eliminate 2 because it has already come in the subsequence. Now, we will notice the pattern that when first term comes, then second comes if it is not same as the first, maybe we take a set because it allows first term to enter but on later, we can eliminate its usage by using find function. Also, we will keep a track of all values within array which are not repeated. Now, the question is whenever I am taking 2, I have a series, similarly for 3, and so on. So, now we calculate from last point and track all points same as first occurrence. Now, lets build a suffix array, we have build it to track the number of subarrays that we track from index i to n-1. Like it is to track allowed subarrays taken from back i.e. last. Now, we will iterate a loop from 0 to n, now in suffix array, we had a lock on j items that they shouldn't be included. Now, lock is on first item that if first is true, then we will add the total number of subarrays to be returned as answer.

Approach:
We just need to traverse from both sides, then create a lock at jth level in subarray sum and finally at ith level to get final subarray.

Time Complexity: O(n)

Code:
```bash
#include <bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        vector<int>arr(n);
        for(int i=0; i<n; i++){
            cin>>arr[i];
        }
        set<int>first, last;
        vector<bool>isFirst(n, false), isLast(n, false);
        for(int i=0; i<n; i++){
            if(first.find(arr[i])==first.end()){
                isFirst[i]=true;
                first.insert(arr[i]);
            }
        }
        for(int i=n-1; i>=0; i--){
            if(last.find(arr[i])==last.end()){
                isLast[i]=true;
                last.insert(arr[i]);
            }
        }
        vector<int>suff(n+1, 0);
        for(int i=n-1; i>=0; i--){
            suff[i]=suff[i+1]+(isLast[i]?1:0);
        }
        long long sum=0;
        for(int i=0; i<n; i++){
            if(isFirst[i]){
                sum+=suff[i];
            }
        }
        cout<<sum<<endl;
    }
}
