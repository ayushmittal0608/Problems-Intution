# Number of Paths with Max Score

E 2 3
2 X 2
1 2 S

We need to find path with max score and number of ways required for achieving that score. Now, we need to start from S and reach E and if X comes in between, then we should not traverse this path, while if there is a path, then we need to find the max score path, so if we go from S->2->1->2->E, we will have 5 as max score and when we traverse S->2->3->2->E, we will have 7>5 as max score. Now, how can we find it??

Since we need to start from S, we start from i=n-1 and j=n-1 and traverse each i and j from n-1 to 0, to reach E. So, currently we will be having a currScore which stores our current array traversing from j=n-1 to j=0, at some i, let's say i=n-1, now when it goes from i=n-1 to i=n-2, we need to store values of currScore in another array which is nextScore, where at jth position, we have down direction, j+1th position, we have diagonal direction and at currScore's j+1th position, we have right. So, now if X is present at that position, we continue and if E is present at that position, then we have nothing to add in their max score and if there is some value then we will add that value inside the max({currScore[j+1], nextScore[j], nextScore[j+1]}), which is stored inside currScore for that particular j and that moves to nextScore once that j for i reaches to 0, so that we could again calculate the max score till that value in a path. If we get those values, then we add ways inside it that there are 2 best scores, so we have 2 ways to reach there, hence it is 2 but if till global ways, we have 1 max score, then we return 1 way because best way is yielded from all the 3 directions having that best value. Now, let's say instead of X there is 3,

E 2 3
2 3 2
1 2 S

Now, at 3, we have two ways either from S->2->3->2->E or S->2->3->2->E, so now at 2, we yield max score from 2 ways since it is equivalent to best in two ways, so finally, we will be having 2 as number of ways.

```
vector<int>nextScore(n+1, -1);
vector<int>nextWays(n+1, 0);
for(int i=n-1; i>=0; i--){
  vector<int>currScore(n+1, -1);
  vector<int>currWays(n+1, 0);
  for(int j=n-1; j>=0; j--){
    char cell=board[i][j];
    if(cell=='X'){
      continue;
    }
    if(cell=='E'){
      currScore[j]=0;
      currWays[j]=1;
      continue;
    }
    int best=max(currScore[j+1], nextScore[j], nextScore[j+1]);
    if(currScore[j+1]==best){
      ways+=currWays[j+1];
    }
    if(nextScore[j+1]==best){
      ways+=nextWays[j+1];
    }
    if(nextScore[j]==best){
      ways+=nextWays[j];
    }
    int value=(cell=='E')?0:cell;
    currScore[j]=best+value;
    currWays[j]=ways;
  }
  nextScore.move(currScore);
  nextWay.move(currWay);
}
if(nextScore[0]==-1){
  return {0, 0};
}
return {nextScore[0], nextWays[0]};
```

Mental model is simple, one state is for storing prev state and other for curr state and then traversing across all 3 paths - down, right, and diagonal based on conditions and similarly for number of ways. This way we will be able to calculate both maxScore at E and number of ways to achieve it till E.








