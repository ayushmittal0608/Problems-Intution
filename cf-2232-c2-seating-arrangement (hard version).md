# Problem
This is the Hard version of the problem. The difference between the versions is that in this version, the constraints on n, x, s, t are larger. You can hack only if you solved all versions of this problem.

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
Each test contains multiple test cases. The first line contains the number of test cases t (1≤t≤104). The description of the test cases follows.
The first line of each test case contains three integers n, x, and s (1≤n,x,s≤2⋅105) – the number of Alice's friends, the number of tables, and the number of seats per table. The second line contains a string u of length n
 consisting only of the letters A, E, and I, representing an ambivert, extrovert, and introvert respectively.

It is guaranteed that the sum of n for all test cases is at most 2⋅105.

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

# Problem Intution:
This question explains the magic of codeforces that I don't think most of the people have noticed. We generally think that solution of easy and hard version of cf is different. When I solved this problem, I got enlightened on the conclusion that CF is not about knowing algorithm and implementing it but it is all about problem solving and critical thinking.

We know that if a person is an introvert, we take seat+=(s-1) which means acquire one seat from empty table and do table--, then update ans which means invitation granted, then comes the extrovert where if seat>0, then we decrease the number of seats and increase the ans which means invitation granted as he wants to sit with someone. Now, if there is no seat available, then he checks which seat as someone, so he finds the ambivert and that ambivert has increased a share/help to him, so if share/help>0 and table>0, then both are decreased and seat becomes seat+=(s-1) and invitation granted. Now, comes the ambivert, so if seat>0, then decrease the seat and increase ans and share/help which means invitation granted, now if seat becomes 0, then if table>0, then decrease the table and make seat+=(s-1) and hence invitation granted, ans++. Finally, we get the ans.

Now, the beauty and magic of CF is that if we solve this problem using this approach, we can copy the same code to cf-2232-c1 (easy version) and we will get it accepted by CF and I think if we know this approach, we could be able to solve 2 problems without taking care of constraint problem. After watching and solving such problems, CF attracts me more to solve more problems and participate in more contests.

# Code:
```
for(int i=0; i<n; i++){
  if(a[i]=='I'){
    if(table>0){
      table--;
      seat+=(s-1);
      ans++;
    }
    else if(a[i]=='E'){
      if(seat>0){
        seat--;
        ans++;
      }
      if(table>0 && count>0){
        count--;
        table--;
        seat+=(s-1);
        ans++;
      }
    }
    else if(a[i]=='A'){
      if(seat>0){
        seat--;
        count++;
        ans++;
      }
      if(table>0){
        table--;
        seat+=(s-1);
        ans++;
      }
    }
  }
  cout<<ans<<endl;
}
```











