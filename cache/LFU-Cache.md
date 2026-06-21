## LFU Cache
This is the second type of cache which is an advanced version of LRU Cache where we solve major drawbacks of LRU Cache which was only fetching the data based on the recent access. But this cache is specifically built to consider the frequency of the number of times, we have accessed the data. Let's say we are given to build LFU Cache and we may argue and implement inside LRU Cache, the frequency and increase it inside the cache and mpp[key] but let's say we have done it but is it a real LFU Cache? Because then it would be just an element being stored which is tracking frequency. So, it will be more of a frequency tracker rather than LFU cache until and unless we are not moving it to the top based on frequency.

Let's think of it for sometime that we can do, let's say initially, we have a freq as 1 when we are setting a cache, now in that freq, what if we place a node containing key and value, so let's say it is mpp[1].push_front({key, value}). Now, we know if freq reaches to 2, then we will remove or erase it from 1 and place it inside 2 but know question arises frequency of what? So, as we know that while setting data into a cache, we have set(key, value) function and for getting data from cache, we have get(key) function. So, we also need to manage a cache[key] which stores latest frequency record, i.e. mpp[1].begin(). Now, the question arises that what if our capacity would get filled and a key need to be evicted which has least frequency. So, we also need a minFreq to evict the least frequently used data to maintain data within a capacity.

```
class Node{
  int key, val, freq;
  Node(int key, int val){
    key=key;
    val=val;
    freq=1;
  }
};
```

```
class LFUCache {
  unordered_map<int, pair<Node>>mpp;
  unordered_map<int, pair<Node>>cache;
  int get(int key){
    ...
  }
  void put(int key, int val){
    ...
  } 
};
```


```
void put(int key, int val){
  if(capacity==0){
    return;
  }
  if(cache.find(key)!=cache.end()){
    cache[key]->val=val;
    get(key);
    return;
  }
  if(cache.size()==capacity){
    auto node=mpp[minFreq].back();
    cache.erase(node.key);
    mpp[minFreq].pop_back();
    if(mpp[minFreq].empty()){
      mpp.erase(minFreq);
    }
  }
  mpp[1].push_front(Node(key, val));
  cache[key]=mpp[1].begin();
  minFreq=1;
}
```

Now, for getting a node with a key, if there is no key inside cache, then it return -1, but if there is a key, then we store it as node and then remove it from mpp[freq] and if it is empty, then we erase it from mpp and if our minFreq was equal to that freq, we increase the counter for minFreq to shift a window one forward. Obviously, we know that if we insert any value, it should first have to reach 1, then it should move forward. So, once it is done, then we increase the freq of node and at that freq we push the node at front inside mpp and same store it inside cache, then return the value of that key.

```
int get(int key){
  if(cache.find(key)==cache.end()){
    return -1;
  }
  auto it=cache[key];
  int val=it->val;
  int freq=it->freq;
  Node node=*it;
  mpp[freq].erase(it);
  if(mpp[freq].empty()){
    if(minFreq==freq){
      minFreq++;
    }
  }
  node.freq++;
  mpp[node.freq].push_front(node);
  cache[key]=mpp[node.freq].begin();
  return val ;
}
```

Now, let's build a mental model for it, when we closely note it, we will get to know that we need frequency and we also need key, so the base condition for put(key, value), capacity can be 0 or it can cache.size() can be equal to capacity, hence eviction and also, if there is already a key inside mpp. Same is for get(key) where if we don't find a key, we return -1, else we store freq and val to be used by minFreq and return finally. Then, we have address to it as node which we remove from mpp[freq] and if it becomes empty and minFreq is equal to freq, then we need to shift it up to slide a window, and hence increase the freq of node and push it inside mpp[node.freq] and inside cache[key].

For building low latency algorithms, cache plays a really important role where class or struct based templates are preferred over linked list for their cache friendliness, and ring buffers are being used in place of queues for achieving low latency, as linked list and queues are the connected nodes, where each node is separately allocated and is scattered in memory, while arrays are more closely placed near to the data to be fetched.



