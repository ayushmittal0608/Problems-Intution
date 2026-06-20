## LRU Cache

Let's think about LRU Cache that how is it being implemented? The one part of building LRU cache is to set the cache at some key with some value and second part is to get the requested key. Once we know this, we have solved a major part of building LRU Cache, now obviously we know that we need to add a key at the front, but still we want to manage each key-value inside a map as mpp[key]=cache.begin() or newNode. Why are we managing the nodes inside mpp? Let's focus on the trade-offs when we use an LRU Cache. 

We know that an edge case may exist that key already exists in a cache. Now, in typical LRU cases that we used to discuss and implement as a part of learning, we don't question that why is it always that if key already exists in mpp, we remove it from last and insert it at front. Now, there are n number of cases where such thing can't exist, for eg, if we are changing the existing key and bring it to the top, now if we don't take the existing key and generate a new key, our previous key will contain a stale data which is being served inside the rendered data. Now, there are two ways out of it: if we find a key already, we add new data and set it to front and remove it from cache and the other case would be that if we find a key already, it contains a data, what if we insert new data in same key, now while rendering it fetches the latest data from the cache and if it doesn't able to fetch new data, it would serve stale data for ensuring high availability.

The other edge case is that if the capacity of cache gets filled, then we will remove the last data from cache and mpp. So, if we break the crux of LRU Cache, we realise it is not that hard to implement.

Let's build it:

```
class LRUCache() {
  unordered_map<int, pair<int, int>>mpp;
  list<pair<int, int>>cache;
  int capacity;

  LRUCache(int cap){
    capacity=cap;
  }
};
```

Now, we have a main function where we know what to design because that we have already constructed. So, we are just calling the functions and setting the value to key and getting the key.

```
int main(){
  LRUCache LRU(5);
  LRU.set(1, 1);
  LRU.set(2, 2);
  cout<<LRU.get(1)<<endl;
}
```

Now, let's design set and get functions for setting key as 1 and value as 1 and then getting the key as 1.

```
int get(int key){
  if(mpp.find(key)==mpp.end()){
    return -1;
  }
  auto it=mpp[key];
  int value=it->second;
  cache.erase(it);
  cache.push_front({key, value});
  mpp[key]=cache.begin();
  return value;
}

void set(int key, int value){
  if(mpp.find(key)!=mpp.end()){
    cache.erase(mpp[key]);
  }
  else if(cache.size()==capacity){
    auto last=cache.back();
    mpp.erase(last.first);
    cache.pop_back();
  }
  cache.push_front({key, value});
  mpp[key]=cache.begin();
}
```

So, let's build a mental model to build a cache, like first is to build a cache class, then define the capacity inside the class, also take parameters like unordered_map<int, pair<int, int>> and list<pair<int, int>>. Then inside the main function, we initialise a cache, set key and value and get the key whenever required.

Now, while setting a cache, we have two edge cases that we generally face, these are not edge cases, these are the problems someone face inside the production for cache, where either key already exists or capacity gets filled. Initially, we push {key, value} to front of cache and mpp[key]=cache.begin(). Then if key already exists, we remove the mpp[key] from the cache, if capacity gets filled, we fetch the last element from back of cache and erase it from mpp and pop the cache from back, which removes the last key from mpp and cache.

Now, while getting a cache, if key doesn't exist, we return nothing but -1, but if it exists, then we fetch the value from mpp[key]->second and remove the mpp[key] from back to insert it at front and update mpp[key] with cache.begin(). Then finally, we return the value.

The time and space complexity for both the processes are O(1).












