You are given a string s of length n, consisting of lowercase Latin letters, and an integer k. You need to check if it is possible to remove exactly k characters from the string s in such a way that the remaining characters can be rearranged to form a palindrome. Note that you can reorder the remaining characters in any way. A palindrome is a string that reads the same forwards and backwards. For example, the strings "z", "aaa", "aba", "abccba" are palindromes, while the strings "codeforces", "reality", "ab" are not.

Input
Each test consists of multiple test cases. The first line contains a single integer t (1≤t≤104) — the number of the test cases. This is followed by their description.
The first line of each test case contains two integers n and k (0≤k<n≤105) — the length of the string s and the number of characters to be deleted.
The second line of each test case contains a string s of length n, consisting of lowercase Latin letters.
It is guaranteed that the sum of n over all test cases does not exceed 2⋅105.

Output
For each test case, output "YES" if it is possible to remove exactly k characters from the string s in such a way that the remaining characters can be rearranged to form a palindrome, and "NO" otherwise.
You can output the answer in any case (uppercase or lowercase). For example, the strings "yEs", "yes", "Yes", and "YES" will be recognized as positive answers.

Intution:
  We generally think that this is palindrome+reordering question but actually reordering+removal has eased out this problem more. Let's say if it is a removal problem only, we have to take longest palindromic subsequence where we check the non equal characters by excluding i and j to get which one to remove and adding 2 to the dp when both the elements are equal. But here the scenario is different, we just want reordering+removal, so we know k is the limit, so we use k as a limit. Let's say there is a string, it has a freq of all numbers as even, then it is an even number, if it has odd number of terms and we can remove k, and we know that we can remove them till k, so we say it's ok, return yes that we can easily manage to reorder and remove to find palindrome. If it is an odd number, then we can have multiple even counts but there exists a number whose frequency is odd, now assume if there are 2 or more such numbers, what will happen, we need to remove them, so we have two of the cases - either odd or even both depends on odd count but we are not segregating, we just want palindrome no matter how. So, its a pretty easy problem to solve.

Approach to Solve:
We can easily design a code for it like we know that we need a freq(26, 0) and then add elements to it, with freq[elements-'a']++, then once we get it we loop on freq and find odd count and then odd count controls everything as we just want palindrome and no label like its an even or odd, we don't care actually.

Complexity Analysis:
- Time: O(n)
- Space: O(1)

Code:
```bash
#include <bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n, k;
        cin>>n>>k;
        string s;
        cin>>s;
        vector<int>freq(26, 0);
        for(char ch:s){
            freq[ch-'a']++;
        }
        int odd_count=0;
        for(int f:freq){
            if(f%2==1){
                odd_count++;
            }
        }
        if(odd_count-1<=k){
            cout<<"Yes"<<endl;
        }
        else {
            cout<<"No"<<endl;
        }
    }
}
