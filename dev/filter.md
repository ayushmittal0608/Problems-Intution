For eg, I go to google and search something inside the search engine. So, we might wonder that google search engine uses trie algorithm with frequency for storing each record, the latest frequency topics at the top. Let's not assume anything about what is being used in google search engine or not. If for eg, Ayush or any developer try to build google, what can they think before building it? Maybe that old trie algorithm one or this javascript based filter function and it comes with the intution that we can use it over here. Maybe those people were having more knowledge in terms of they having used trie and we don't know whether our approach is much feasible or not but we can atleast try. Maybe those people could also think that they might solve it this way.

For searching or filtering anything from a huge bunch of data, we are like 

```data.filter(engine => engine.search.toLowerCase().includes(searchQuery.toLowerCase()))```

We don't know the element that we have searched in a search box is present or not but when we click on search button or our e.target.key is enter key, then for eg, I have written `My name is Ayush Mittal`, so totalCount will be 2^5 - 1, so we have mask from 0 to totalCount and to have all the possible subsequences, we will be having something like:

const allSubsequences = useMemo(() => {
  const N = word.length;
  const totalCount = 2^N-1;
  const result = new Set();
  for(let mask = 0; mask < totalCount; mask++){
    let subSeq = '';
    for(int i=0; i<N; i++){
      if(mask & (1<<i)){
        subSeq+=word[i];
      }
    }
    result.add(subSeq);
  }
  return Array.from(result);
}, [word]);
```

Now, we are having too many combinations around 2^N - 1 which we are storing inside DB and then using

```
searchQuery.map((search, idx) => (
  <div key={idx}>
    <p>{search.items}</p>
  </div>
))
```

Now, we are training the search engine with our data, which is getting stored as words and phrases with frequency. This is the creation from different angle. I don't know whether people have noticed such thing or not but I love to solve problems through different angles. Maybe this is not the most feasible approach but better than not trying anything.

Now, whenever in an input search box, we search anything, it saves searchQuery as onChange={(e) => setSearchQuery(e.target.value)}, so for every e value, it is search element from the above box and when we click enter, it gets saved in DB.

Now, what if the search results doesnt exist for that search? So, we will take it as a noise and remove it from that DB and send to another audit DB, to fetch data related to that topic whose search is not available and is blogged and that url is being listed on search.

If we closely look into how this whole searching and filtering is done needs a lot more GPU for searching and filtering, so we need a context regarding each and every prompt, so that we can implement indexing at various places. I don't know why my innocence and ignorance is taking me to building something like AI. This approach takes around exponential storage for storing data as approx 2^N for each record.

This approach is leading us to some creation inside the fields like NLP, DNA sequencing, etc. and this is the way maybe how vectorDB is being designed to build an AI model. Let's not enter AI as a subject, let our innocence and ignorance drives us to some creation because repetition can come if we follow certain model and build it that way understanding that approach but real creation always occur when we reject the repetition and let our ignorance drives us to derive something.
















