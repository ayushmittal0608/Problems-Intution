# Find the Safest Path in a Grid

0 0 1
0 0 0
0 0 0

Now, this grid is given to us and we need to find the maximum safeness factor of all paths leading to n-1, let's dissect this statement first.
So, it implies=>
    Path-1: 1->2->3->4->5, so minimum here is 1
    Path-2: 2->3->4->5->6, so minimum here is 2
So, safeness factor of 2 > safeness factor of 1

Now, these paths are not grid paths but manhattan distance from any cell in the path to any thief in a grid. Since, we need to find minimum manhattan distance, so in path with safeness factor of 2, 2 is the minimum value.

Maximum safeness factor path but with minimmum safeness factor within the single whole path and problem gets solved.

# Calculation of Manhattan Distance
Let's take a 2-D dist array. Now, we just need to take care of one thing that all elements inside it are currently INT_MAX. Why? Because we need to calculate manhattan distance for all positions from the thief position.

```
vector<vector<int>>dist(n, vector<int>(n, INT_MAX));
bfs(grid, dist, n);
```

Now, inside bfs, we store the thief position inside a queue so that we can calculate manhattan distance with respect to that thief position and assign dist to the queue.

```
queue<pair<int, int>>q;
for(int i=0; i<n; i++){
    for(int j=0; j<n; j++){
        if(grid[i][j]){
            dist[i][j]=0;
            q.push({i, j});
        }
    }
}
```

Now, we have a queue with positions i and j and dist at that pos is 0, because manhattan distance from itself is always 0. Now, let's traverse different paths.

```
vector<int>row={-1, 1, 0, 0};
vector<int>col={0, 0, 1, -1};
while(!q.empty()){
    int x=q.front().first;
    int y=q.front().second;
    q.pop();
    for(int i=0; i<4; i++){
        int newX=x+row[i];
        int newY=y+row[j];
        if(newX>=0 && newX<n && newY>=0 && newY<n && dist[newX][newY]>1+dist[x][y]){
            dist[newX][newY]=1+dist[x][y];
            q.push({newX, newY});
        }
    }
}
```

# Calculation of Minimum Distance In Path With Maximum Safeness Factor

In order to maximise safeness factor path, we will take a path with highest safeness factor to traverse on priority, so we will take a max heap which is the most important part.

We might consider this problem as the toughest when we observe only the code complexity but when we watch this problem as some other random broilerplate with more focus on array or grid taken INT_MAX initially or maxHeap/minHeap taken, then it makes the problem too easy to be solved.

```
priority_queue<pair<int, pair<int, int>>>pq;
pq.push({dist[0][0], {0, 0}});
```

Now, we need to calculate the minimum safeness factor with maximum safeness factor path, so we make pq empty and traverse the new path over newX and newY in all 4 coordinates taking priority as priority, and we will reach the final value at coordinates (n-1, n-1).

```
vector<vector<bool>>vis(n, vector<bool>(n, false));
while(!pq.empty()){
    int dis=pq.top().first;
    int x=pq.top().second.first;
    int y=pq.top().second.second;
    pq.pop();
    vis[x][y]=true;
    if(x==n-1 && y==n-1){
        return dis;
    }
    for(int i=0; i<4; i++){
        int newX=x+row[i];
        int newY=y+col[i];
        if(newX>=0 && newX<n && newY>=0 && newY<n && !vis[newX][newY]){
            int d=min(dis, dist[newX][newY]);
            pq.push({d, {newX, newY}});
            vis[newX][newY]=true;
        }
    }
}
return -1;
```

So, now, this problem can be solved within minutes the time we watch this problem and the basics to solve this problem is calculation of manhattan distance at each and every point on a grid with respect to thief.

Now, let's say there is a problem where we are striking a ball to the other balls and when it is of same color, then it bursts all the balls in its contact. How will we do it?

So, now we have this ball as ball[i][j] with i and j in a queue, now if this ball[i][j] is color of the ball and it searches the same color in all four directions and if we found then it stores newX and newY as its color and making all balls in contact as 0 and then those balls will find other balls in contact to make them 0.

```
ball[0][0]='red';
q.push({0, 0});
string color=ball[0][0];
ball[0][0]='';
while(!q.empty()){
    int x=q.front().first;
    int y=q.front().second;
    q.pop();
    for(int i=0; i<4; i++){
        int newX=x+row[i];
        int newY=y+col[i];
        if(newX>=0 && newX<n && newY>=0 && newY<n && color==ball[newX][newY]){
            ball[newX][newY]='';
            q.push({newX, newY});
        }
    }
}

```

Now, in a game like bubble shooter, we have 8 directions, so we will not use [-1, 1, 0, 0] and [0, 0, -1, 1] but we extend it further to [1, 1, -1, -1] and [1, -1, 1, -1], to accommodate all directions.

Now, we will have a specific frame with balls present at non-zero positions or non-'' positions, but we have such positions too, so we need to update our state when ball reaches to a certain position, for eg, it reaches below 'red' or 'green', then it needs to stick there, otherwise move towards the color and not stay in empty zone.

Now, what we will do? Now, we are shooting the ball in specific angle, so it traverse in a straight line motion, if it goes out of screen, it rebounds to change its direction forming same angle of reflection to the angle of incident and stay near to the ball, so we are continuously searching in the straight line path of that ball and ask it, whether it can exist there or not or move forward, so if it traverses to (1, 1) and find nothing at (2, 2), then it moves to (2, 2), then again for (3, 3), now this is a straight line path where we are continuously updating its position like:

x=1, y=1, now it reaches to path 2 and 3, but we have a frame where some colored ball is put at position 2 and 3, so we will put it at (2, 2), so now we have a difference of 1 being left with respect to 3, so either the ball is present at (3, 3) or (3, 2) to make it 0 because we can't compromise on this case and ball may go further from (2, 3) in that case. We will think about the best possibility to build it. Lastly, it has just blown up our mind with a nice thinking approach which is crucial for improving neural networks of our brain as a neural exercise.
