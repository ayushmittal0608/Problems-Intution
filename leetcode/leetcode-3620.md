# Network Recovery Pathway

0 1 5
1 3 10
0 2 3
2 3 4
online = [true, true, true, true], k=10

Now, in this problem, we are having k=10 and the condition is that there should be a path that traverse from 0 to n-1, also it should not exceed k, so the whole path should be less than k. There is one more condition that if it is offline, then we cannot traverse that path, so in the intermediate positions, this offline condition exists which breaks the network.

Now, in order to have clarity over this problem, we need to know what is atleast. The atleast means either k or less than k, so it always lie to the lower bound of a search space while if we want it just above the k but the least one, then it would become upper bound, but in this problem, we want a lower bound, so first snippet is:

```
while(low<=high){
  int mid=low+(high-low)/2;
  if(check(mid,...)){
    ans=mid;
    low=mid+1;
  }
  else{
    high=mid-1;
  }
}
```

Now, in order to apply binary search to a path, we need to sort a path, so we will topologically sort the whole path. For each v, we increase indegree of v as the path continues, and now we know that path always start from u, which we need to push into queue but which u? So, the one whose indegree is 0. Hence, we will sort it topologically.

```
vector<vector<pair<int, int>>>adj(n);
vector<int>indegree(n, 0);
for(auto& e:edges){
  int u=e[0], v=e[1], w=e[2];
  adj[u].push_back({v, w});
  indegree[v]++;
}
queue<int>q;
for(int i=0; i<n; i++){
  if(indegree[i]==0){
    q.push(i);
  }
}
while(!q.empty()){
  int u=q.front();
  q.pop();
  topo.push_back(u);
  for(auto &[v, w]:adj[u]){
    indegree[v]--;
    if(indegree[v]==0){
      q.push(v);
    }
  }
}
```

Now, since we need to find the maximum path score with minimum edge cost, so for maximum path score, our search space would lie between 0 and maxm, so we apply binary search on answer. We can call it by that name but eventually we are traversing the search space and managing to check and reach final outcome. So, low=0, high=maxm.

Now, inside the check function, we have a whole list of topo array where we need to find the minimum edge cost path, so there will be one more snippet to find it which is kind off djikstra but since we have already sorted it, so it would be easy for us to traverse the whole path through topo array.

```
const int INF=1e18;
vector<int>dist(n, INF);
for(int u: topo){
  if(dist[u]==INF){
    continue;
  }
  if(u!=0 && u!=n-1 && !online[u]){
    continue;
  }
  for(auto &[v, w]:adj){
    if(w<mid){
      continue;
    }
    dist[v]=min(dist[v], dist[u]+w);
  }
}
return dist[n-1]<=k;
```

Now, we have listed all the conditions required to check the payload so that binary search could traverse as per the condition to retrieve final outcome of the problem.

So, first condition is that dist[u] should not be INF because initially we have declared it whole as INF, similar case is with intermediate nodes not being online condition, then check over the neighbouring nodes so as to eliminate the values less than mid because we are looking for maximum path score. Now, a question may arise that what if we have some better path which get us to our most optimal outcome if we take w<mid, so now the thinking that is involved in this part of the problem is the optimisation which is already happening through binary search, so we need to concentrate in check function to optimise w<mid, because even if it would give us more optimal path, in next round, if we don't get the most optimal answer, we can reduce our search space to search further, so there will be no problem in that and our problem will remain optimised.

At last, we might wonder that we have used dist[n-1]<=k, so this is being used so that we can check if this condition exists or not because minimum edge weight till dist[n-1] should be less than k for the path to be considered.

So, how to approach such problem??
First look into the constraints of problem, like it is telling us that minimum edge weight is what we need to calculate keeping in mind that till dist[n-1], it should be less than equal to k. We are also given that we need to find maximum path score among the path with minimum edge weight, so now we can model a search space for it from 0 at the lowest end and maxm at the highest end. 

$$ maxm=max(maxm, w) $$

Now, in order to apply binary search to this problem, we need to sort the path topologically to get all the nodes sorted in a defined order to allow binary search to be executed properly. So, now, firstly we are having a particular order in which every node is sorted so that we can traverse each element properly and execute binary search efficiently. This is one way of approaching this problem.

However, this problem can be solved effectively using djikstra algorithm too alongwith binary search, where on check function, we implement djikstra to get minimum edge cost and at last the condition of dist[n-1]<=k and finally we can easily reach to the outcome.

