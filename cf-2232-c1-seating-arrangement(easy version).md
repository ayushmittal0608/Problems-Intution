# Problem
This is the Easy version of the problem. The difference between the versions is that in this version, the constraints on n, x, s, t are smaller. You can hack only if you solved all versions of this problem.

Alice's friends have come to the party, and now they are lining up to enter the party.

There are x tables at the party with s seats each. Each seat can only hold one person.

Each friend has one of these three following personalities:
- Introverts (I) who have to sit at an empty table
- Extroverts (E) who have to sit at a non-empty table
- Ambiverts (A) who can sit at any table.
Initially, every seat is empty. However, because Alice was eating cakes, her friends had already formed a line, which Alice cannot change their order. For each person in the line, Alice has to assign them a table or kick them out of the party. Each person is seated before the next person is assigned a table.

Wanting to have a lot of fun at the party, Alice needs to seat as many people as she can at the party. Help her find the maximum number of friends she can have at the party.

Note that once a friend is seated, they are not allowed to move even if they are not seated according to their personality anymore.

Input
Each test contains multiple test cases. The first line contains the number of test cases t (1≤t≤500). The description of the test cases follows.

The first line of each test case contains three integers n, x, and s (1≤n,x,s≤3000) – the number of Alice's friends, the number of tables, and the number of seats per table. The second line contains a string u of length n consisting only of the letters A, E, and I, representing an ambivert, extrovert, and introvert respectively.

It is guaranteed that the sum of n for all test cases is at most 3000.

Output
For each test case, output an integer: the maximum number of people seated.

Example
Input
```6
5 2 2
EIAIE
20 5 5
AEIEEEEIEAAEIEEEEIEA
8 2 4
AAAAAIEE
8 4 2
AIEAEAAI
8 3 3
AIEAEAAI
4 2 2
IAEE
```
Output
```4
20
7
7
7
4
```
Note
In the first test case, there are 2 tables with 2 seats each. Here is one of the ways to achieve the maximum number of people seated.
- The first person is an extrovert. Since all tables are empty, they have to leave the party.
- The second person is an introvert. Alice can assign them to the first table, which is empty.
- The third person is an ambivert. Alice can assign them to the first table.
- The fourth person is an introvert. Alice can assign them to the second table, which is empty.
- The fifth person is an extrovert. Alice can assign them to the second table, which is not empty.
Thus, four people are seated at the party. This is maximal since there are only four seats at the party.

# Problem Intution
When we read this problem, we realise that if we insert an introvert, then we can insert ambivert and extrovert but introvert wants to be inserted alone on a table while extrovert want someone on a table and ambivert has a practice of both. So, let's feel this question rather than solving it, now condition is for introvert and ambivert, so we place them first and we know that there are x tables, so we initiate a loop from 0 to x inside a loop from 0 to n, why so because we have to place introvert and ambivert on individual seats and increase their seats at individual tables, so we take a[j+1]=max(a[j+1], sit+1), now when the turn of extrovert and ambivert comes, then we accommodate them on rest of the seats, so we take a[j]=max(a[j], sit+1) till sit<j*t, now base cases come where j+1<=x otherwise it would exceed x, for ambivert and introvert and j>0 and sit<j*t otherwise we get it 0 and we won't be able to get right a[j] value for ambivert and extrovert.

# Code
```for(int i=0; i<n; i++){
  vector<int>a=dp;
  for(int j=0; j<=x; j++){
    if(dp[j]==-1){
      continue;
    }
    int sit=dp[j];
    if(p[i]=='A' || p[i]=='I'){
      if(j+1<=x){
        a[j+1]=max(a[j+1], sit+1);
      }
    }
    if(p[i]=='E' || p[i]=='A'){
      if(j>0 && sit<j*t){
        a[j]=max(a[j], sit+1);
      }
    }    
  }
  dp=move(a);
}
int ans=0;
for(int i=0; i<=x; i++){
  ans=max(ans, dp[i]);
}
cout<<ans<<endl;
```
Too easy. Hence, solved.









