Now, we are having a lots of data and we need to organise it in a way that data is retrieved to a table in chunks and not the whole data at the same time, it is being implemented by sending page and limit to backend. But before going into pagination concept, first thing the people use to do is to implement input form in the form of wizard. Our reflexes in some coding or thinking or anything doesn't get formed if we are just skipping the small part and getting to the bigger part. But sticking too much to the small part is the hindrance to the growth of our thinking too. So, we need to first try to implement wizard before pagination.

What is wizard? It is an input form where each step is dependent on previous state. For any rendering inside react.js, first thing that we need to know is the conditional rendering part, for eg, if something is associated with state, we have taken, so we use && like {ayush && <h1>Welcome Ayush!</h1>} and if we want a condition that only display it if ayush is there and otherwise fall to No one found, so we use ? which is like {ayush ? <h1>Welcome Ayush</h1> : <h1>No one found</h1>}.

So, currently we have let's say 4 steps for the form, now first one is step1, so our current state will be 1, so we use state like const [page, setPage] = useState(1); Now we have let's say 4 as maximum pages, so at each button inside that tab, currently if page is 1, then we disable the previous page option and when we get to 4, we disable the next page option. Now, what these buttons are doing, they are just increasing and decreasing the state of page. Now, the page gets changed where we setPages and at each page it loads a different page for input.

```
const [page, setPage] = useState(1);
const nextPage = () => {
  if (page < 4) {
    setPage(page + 1);
  }
};

const prevPage = () => {
  if (page > 1) {
    setPage(page - 1);
  }
};
return(
  {page===1 &&
    <Form1 onPrev={setPrevPage} onNext={setNextPage} disabledPrev={page===1} disabledNext={page===4}>
  }
  {page===2 &&
    <Form2 onPrev={setPrevPage} onNext={setNextPage} disabledPrev={page===1} disabledNext={page===4}}>
  }
  {page===3 &&
    <Form3 onPrev={setPrevPage} onNext={setNextPage} disabledPrev={page===1} disabledNext={page===4}>
  }
  {page===4 &&
    <Form4 onPrev={setPrevPage} onNext={setNextPage} disabledPrev={page===1} disabledNext={page===4}>
  }
)
```

This is how we can design our input form, now for eg, we want n number of such forms, what can we do? So, we need to optimise this form a little more.

```
const [page, setPage] = useState(1);
const forms = {
  1: Form1,
  2: Form2,
  3: Form3,
  4: Form4,
}
const CurrentForm = forms[page];
const nextPage = () => {
  if (page < 4) {
    setPage(page + 1);
  }
};

const prevPage = () => {
  if (page > 1) {
    setPage(page - 1);
  }
};
return (
  <CurrentForm onPrev={setPrevPage} onNext={setNextPage} disabledPrev={page===1} disabledNext={page===4}>
)
```

Finally, we know how to implement wizard. Now, we can easily get intution about how to implement pagination. Now, let's say we have a lots of options which can be 5, 10, 20 or anything and so on.

```
const [limit, setLimit] = useState(10);
const [page, setPage] = useState(1);
function handleLimitChange (e) => {
  setLimit(Number(e.target.value));
  setPage(1);
}
return(
  <select value={limit} onChange={handleLimitChange}>
    <option value={5}>5</option>
    <option value={10}>10</option>
    <option value={20}>20</option>
  </select>
)
```

Now, we have limit and page, so after selecting limit, we can set any page where we send page and limit both to backend to fetch record.

```
const [data, setData] = useState([]);
const [totalPages, setTotalPages] = useState(1);
async function fetchData (page, limit) {
  fetch(`/api/data?page=${page}&limit=${limit}`)
  .then((res) => res.json())
  .then((data) => { setData(data.data); setTotalPages(data.totalPages) })
  .catch((err) => console.log(err));
}
useEffect(() => {
  fetchData(page, limit);
}, [page, limit])
```

Finally, we have reached to a place where we can now easily implement pagination as we have got the intution to implement this pagination concept. Now, one more thing arises that if page is 1, then obviously it has a limit of 10, but we need an offset. Now, what is an offset? Let's say limit is 10, so we retrieve first 10 records, now if there will be no offset, then on next page too, we will get same records because limit is 10 but no shifting in records, only first 10 every time. Hence, we need offset too in backend.

```
const offset = (page - 1) * limit;
const data = await db.select().from(data).limit(limit).offset(offset);
```

Now, we might say that totalPages will be totalRecords/limit but we need a ceil value of it, for eg, if there are 104 records, then we will have 11 pages which is equivalent to Math.ceil(totalRecords/limit).

This way pagination will become too easy for us to implement. It has not only covered the pagination concept but also the wizard concept too.

Now, let's go one step forward too. Now, we don't want these buttons and want pagination as infinite scroll. So, we need a retry button after say 20 records scrolling, so when we click that retry button, it setLoading as true and then increase the page by 1, so it would setPage(page+1), now once this loader reaches totalPages, then we won't have such retry button in UI and this way can be implemented easily.

This is basic version of infinite scroll implementation, but in broader aspect comes the addEventListener and removeEventListener, so we have event listener for clicks, scroll and so on. Here, we are using scroll as an event listener, so when window.innerHeight(height of screen) + window.scrollY(amount of Y being scrolled downwards) >= document.body.offsetHeight(totalHeight being scrolled) - 100, where we leave 100px to instruct our scroll to setPage((prev) => prev+1).

Let's not get too deep, because I know there is no people watching it, but still if I need to explain it to a person who doesn't know anything about it, for them, it might intrigue them and be curious to know and for some people, it would be too difficult to handle event listener part. That's why one needs to learn HTML, CSS and JS in depth to reach to the beauty of react.js, node.js, ORM, tailwindCSS, etc.

If we knows the concept well, we are just left with playing in development rather than focussing on learning the concepts for the sake of learning. So, we just need to realise the beauty of everything being implemented and used.







