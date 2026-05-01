Berland is a country with ancient history, where roads were built and destroyed for centuries. It is known that there always were n cities in Berland. You also have records of t key moments in the history of the country, numbered from 1 to t. Each record contains a list of bidirectional roads between some pairs of cities, which could be used for travel in Berland at a specific moment in time.

You have discovered a time machine that transports you between key moments. Unfortunately, you cannot choose what point in time to end up at, but you know the order consisting of k moments in time ai, in which the machine will transport you. Since there is little time between the travels, when you find yourself in the next key moment in time (including after the last time travel), you can travel on at most one existing road at that moment, coming out from the city you were in before time travel.

Currently, you are in city 1, and the time machine has already transported you to moment a1. You want to reach city n as quickly as possible. Determine the minimum number of time travels, including the first one, that you need to make in order to reach city n.

Input
The first line contains two integers n and t  (2≤n≤2⋅105,1≤t≤2⋅105) — the number of cities in Berland and the number of records about key moments in history. Then follows the description of each of the t records.
The first line of each record description contains a single integer mi (0≤mi≤min(n(n−1)2,2⋅105)) — the number of roads in the i-th record.
Each of the next mi lines contains two integers vj and uj (1≤vj,uj≤n, vj≠uj) — the numbers of cities connected by the j-th road in the i-th key moment in history.
The next line contains a single integer k(1≤k≤2⋅105) — the number of time moments between which movements will occur.
The next line contains k integers a1,a2,…,ak(1≤ai≤t) — the time moments at which you will be after each movement.
It is guaranteed that the sum of mi does not exceed 2⋅105. It is guaranteed that each unordered pair (u,v) occurs in the road description for one record no more than once.

Output
Output a single integer — the minimum number of time travels required to reach city n from city 1, or −1 if it is impossible. Note that movement to time moment a1 is also considered a movement.


Intution: 
Here, the question is asking to find minimum time travel and we are given edges, time intervals and teleported time. The intution to solve this question is that since it is having u and v, we need graph algorithm and since we need to find shortest path, we use djikstra's algorithm. It's a three dimensional problem where u and v are mapped to a record of key moments and we know that k moments can occur in time ai. So, we input a[i] and store next moment of a[i] as (i+1). Now, what is happening is we are taking u and find neighbour of u which is v and to [u, v] is mapped a key moment. Now the real game starts. Now, we will find the lower bound of that edgeTime inside next and minimise it. We are actually finding lower bound of next at the edgeTime of u and v. Then, we adjust store it in temp and adjust its value, then put it inside dist[v] to find next element as usual and push dist[v] and v inside set. Then, we will get the minimum time interval as it is that temp only which is the lower bound of next array.

edgeTime[{u, v}].push_back(j+1); <- this j+1 is the key moment in edgeTime for respective u, v
next[a[i]].insert(i+1); <- used over here inside next to find minimum number of travels as we have just given i+1, normal numbers mapped to it.

Approach:
We take first element and its weight in a priority queue and then while it is not empty, we take first node and pop it and then find its neighbour, then compare v and wt with that of u through dist array and if its less we push it in priority queue and update dist and finally return out dist, if n is int_max, return -1 else return dist[n]. Same as intution.

Time Complexity: O(E log k) => it is getting relaxation each time we erase elements from set leading to log k.
In worst case, it can even lead to TLE => O(n^2 t log k)

```bash
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n, t;
    cin>>n>>t;
    vector<vector<int>>graph(n);
    map<pair<int, int>, vector<int>>edgeTime;
    for(int j=0; j<t; j++){
        int m;
        cin>>m;
        for(int i=0, u, v; i<m; i++){
            cin>>u>>v;
            u--;
            v--;
            graph[u].push_back(v);
            graph[v].push_back(u);
            edgeTime[{u, v}].push_back(j+1);
            edgeTime[{v, u}].push_back(j+1);
        }
    }
    int k;
    cin>>k;
    vector<int>a(k);
    for(int i=0; i<k; i++){
        cin>>a[i];
    }
    vector<set<int>>next(t+1);
    for(int i=0; i<k; i++){
        next[a[i]].insert(i+1);
    }
    vector<int>dist(n, 1e9);
    dist[0]=1;
    set<pair<int, int>>sp;
    sp.insert({dist[0], 0});
    int temp;
    while(sp.size()){
        auto [d, u]=*sp.begin();
        sp.erase(sp.begin());
        if(dist[u]<d){
            continue;
        }
        for(auto v:graph[u]){
            temp=1e9;
            for(auto pos:edgeTime[{u, v}]){
                if(next[pos].lower_bound(d)==next[pos].end()){
                    continue;
                }
                temp=min(temp, *next[pos].lower_bound(d));
            }
            temp++;
            if(dist[v]>temp){
                dist[v]=temp;
                sp.insert({temp, v});
            }
        }
    }
    if(dist[n-1]==1e9){
        dist[n-1]=0;
    }
    cout<<dist[n-1]-1<<endl;
}
