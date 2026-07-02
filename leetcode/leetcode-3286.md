# Find a Safe Walk Through a Grid

0 1 0 0 0
0 1 0 1 0
0 0 0 1 0

health=1

Now, we have a grid which is given and health, now we need to traverse this whole grid and if grid[i][j]==1, then reduce health by 1 and we also need to maintain health>0. Also, we return true if we safely reach (m-1, n-1).

Let's build a broilerplate because we know that we need to traverse the whole of the grid, so broilerplate goes like:

```
queue<pair<int, pair<int, int>>>q;
q.push(grid[0][0], {0, 0});
while(!q.empty()){
    int dist=q.front().first;
    int x=q.front().second.first;
    int y=q.front().second.second;
    if(x==n-1 && y==m-1){
        return true;
    }
    for(int i=0; i<4; i++){
        int newX=x+row[i];
        int newY=y+col[i];
        if(newX>=0 && newX<n && newY>=0 && newY<m){
            // writing the whole logic on what to do
        }
    }
    return false;
}
```

Now, currently we will firstly find startHealth which is health-grid[0][0], and if it is less than or equal to 0, it is not positive and we return false. Maybe it is 0, so if it is already 0, we have full health retained otherwise we increase health by 1. So, rather than grid[0][0], we send startHealth inside queue to be used further.

```
int startHealth=health-grid[0][0];
if(startHealth<=0){
    return false;
}
queue<pair<int, pair<int, int>>>q;
q.push({startHealth, {0, 0}});
```

Now, what will be inside this template:

```
if(newX>=0 && newX<n && newY>=0 && newY<m){
    // writing the whole logic on what to do
}
```

So, we do the same for newX and newY positions where our newHealth becomes dist-grid[newX][newY] and if newHealth>0, then we will push inside the queue, else we move forward.

```
if(newX>=0 && newX<n && newY>=0 && newY<m){
    int newHealth=dist-grid[newX][newY];
    if(newHealth>0){
        q.push({newHealth, {newX, newY}});
    }
}
```

Ok, so we have written the whole code and we know that we have written the right code and also the code is correct, but now comes the beauty of compiler while gives us reality check that you need to store memory somewhere as memory limit has been exceeded. Now, we will think off pruning by maintaining a state, so we store it somewhere, let's say prune array. So,

```
vector<vector<int>>prune(n, vector<int>(m, -1));
prune[0][0]=startHealth;
```

```
if(newX>=0 && newX<n && newY>=0 && newY<m){
    int newHealth=dist-grid[newX][newY];
    if(newHealth>prune[newX][newY] && newHealth>0){
        prune[newX][newY]=newHealth;
        q.push({newHealth, {newX, newY}});
    }
}
```

This shows that even compilers and hardwares know the value of help and support but we can't, maybe we are the most smartest people in the world and maybe our smartness lies to our realisation of smartness only because everyone else thinks they are the smartest, so only we can call ourself as the smartest because others would call them the smartest.

Now, what the compiler is doing is that it says that hardware is having a limit for memory, it needs an array to finally get to the result, it is going insane, so it has accepted it's limit. Maybe existence of no pruning could solve the maximum problems of programming but still there lies a beauty in the imperfection of hardware that it assigns job to a new array to help him due to memory limit being exceeded, but I know humans are so cruel, in order to prove their smartest in their mind, they won't accept this imperfection, but it is fine.

This is how we have solved this problem and have learnt the beauty of hardware in its imperfection that enables it to help an array assigning a job, escaping the cruelty of this world. What we can do is just bow down in front of hardware in view of its respect.
