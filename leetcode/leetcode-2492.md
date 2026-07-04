# Minimum Score of a Path Between Two Cities

In this problem, we need to calculate minimum score of path to which we are traversing, even if we have some shortest path, we will ignore that and traverse the path minimum score, for eg.
roads = [[1,2,2],[1,3,4],[3,4,7]], where we traverse from 1->2->1->3->4 just because we are having minimum score when traversing from 1 to 2.

So, now we know that traversal would start from 1 only but it takes all of its neighbouring nodes and calculate the minimum weight or path score. So, we traverse each neighbouring node, minimising it till we get the minimum path score, it means traversing the whole path in such a way that we can obtain minimum path score.

```
vector<vector<pair<int, int>>>adj(n);
for(auto& e:roads){
  int u=e[0], v=e[1], w=e[2];
}
queue<int>q;
vector<bool>vis;
q.push(1);
vis[1]=true;
int ans=INT_MAX;
while(!q.empty()){
  int node=q.front();
  q.pop();
  for(auto& [v, w]:adj[node]){
    ans=min(ans, w);
    if(!vis[v]){
      vis[v]=true;
      q.push(v);
    }
  }
}
return ans;
```

This is the super simple implementation for this whole problem. Now, we might think that what if we just minimise the answer, maybe we could get a very very super simple implementation but what if the nodes are not connected?? Then we can't traverse the min node but it would be there in the matrix, so then it would fail completely.







