Let's see how can we make development to easy to implement, like there are too many individuals who doesn't belong to development side but they are fascinated on how the developers write the codes efficiently and execute them, connecting frontend, backend and db.

So, in order for someone to understand the real development, if someone has knowledge of basic functions like how at each button, we call a function and how is it executed and how can we set state. For eg, we are having an input form and we want to fill it, know its value keeps on changing when we prompt something inside the input box. So, we need a state to manage it, where we use react hooks (useState) which setState of the value. Now, this is not a big challenge to know and code is super simple too but when someone is approaching it for the first time, they might get stuck into the type of payload inside the state, for eg, const [ayush, setAyush] = useState(?), so this ? can be null, boolean, empty string (""), empty object ({}), empty array ([]) or undefined. Now, null is used when it is completely empty while undefined is being used when it is taking a default value. So, one needs to know about which parameter we want to set as ayush. Now, comes the part where real engineering comes which if we know, we could be able to understand the whole development in one go. This one trick can solve whole development and now, anyone can build their websites and enjoy coding.

Let's say we have an input form for filling an input values like name, email, phone, so inside html tag that we have returned in our component or function, we will just do one thing <input type="text" value={ayush} onChange=((e) => setAyush(e.target.value))>. Now, this line `onChange=((e) => setAyush(e.target.value))` is the real essence of whole development which is known as callback. Once anyone would know what is callback, they could be able to atleast build a basic website though not with that scalability, but still to make them happy.

Now, here, e is the targetted event, which is a state, set as a value, then another target is set as a value and so on, this builds the whole ayush. So, it is like once e is set, then implement next target to set in ayush, then that is inside the e, then implement next target to set as ayush. This way we will be able to get ayush. Now, we have a button which we click on, it calls the function onClick={handleTarget} and inside this function, we will send the payload to backend.

```
const handleTarget = async () => {
  try {
    const res = await fetch('/api/ayush', {
      method: 'POST',
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({name: ayush})
    });
    if(!res.ok){
      throw new Error(`Server Error - ${res.status}`);
    }
    return res.json();
  }
  catch(err){
    console.log(err);
  }
}
```

Now, here we have used async and await, so what is happening here, let's say if we don't use async or await, so we might get stuck in the execution of only first or we won't be able to get the sequence that we need that requests to backend to be executed in. For eg, I want to send an audit log for creation of ayush and other parameters and we don't use async or await, it would give us an error of promise not resolved during the execution of audit log and we only want that to occur once ayush gets into the route.

Now, since the API type of the payload is JSON, so inside backend, we need app.use(express.json()) to accept JSON payload for rendering where `const app = express();`. Now, comes app.listen(PORT), now I am not using any callback, so I won't be able to get the logs about whether my port is listening on this port or not, so for logging, we need to use callback, that if app listens to port PORT, then only it should log that App is listening to the port: ${PORT}.

```
app.listen(PORT, () => {
  console.log(`App listening on port ${PORT}`);
});
```

In a similar way, we can execute the post to some route. So, everything is callback here like the next function can only be implemented when first one get executed, so it will be like:

```
const fetchA = (() => {
  const fetchB = (() => {
    const fetchC = (() => {
      ...
    }) 
  })
})
```

Now, it might lead to a callback hell for which promises are being implemented to resolve this callback hell problem, like for eg, we have 3 functions to be executed, so we will implement them like:

```
const [resA, resB, resC] = await Promise.all([
  fetchA();
  fetchB();
  fetchC();
  ...
])
```

In a similar way, there is an async and await function which can also be executed in sequence resolving the promise. In backend, it is also utilising promises and all of the development revolves around this concept. If we want to visualise the callback, we can visualise it as a call stack where there is one function inside another, so call stack just keeps it one over the other, so that last function will be first to come out. For eg,

```
const fetchA = (() => {
  console.log('A');
  const fetchB = (() => {
    console.log('B');
    const fetchC = (() => {
      console.log('C');
      ...
    })
    fetchC();
  })
  fetchB();
})
fetchA();
```

So, output will be like ABC

Now, here it is not applying. Why? Because we have called the function after consoling.

This callback hell was an hindrance to the better utilisation of event loops, hence promises were designed inside node.js to handle the functions effectively despite being a single threaded server.

So, if someone understands this part, then anyone can build any small project easily using MERN stack, though I don't use MongoDB and being honestly speaking, I don't have too much hands-on over MongoDB because I have worked more in postgreSQL and drizzle ORM but still one can learn how to implement the things based on development.

Now, the other thing that comes inside development is what to fetch in node.js. Like

```
app.post('/api/fetch', (req, res) => {
  try{
    const { ayush } = req.body;
    return res.status(200).json({ message: success });
  }
  catch(err){
    res.status(500).json({ message: err.message })
  }
  
})
```

now, if it is /api/fetch/:id, then it is fetched as const {id} = req.params;
if it is /api/fetch?name=Ayush&email=mittalayush2003@gmail.com, it is const { name, email } = req.query;

Now, one can easily build whole website, though basic one but can easily build any website now, even the beginner one. One thing more to add is get, let's see how can we execute get method.

```
useEffect(() => {
  fetch('/api/fetch')
  .then((res) => res.json())
  .then((data) => setAyush(data))
  .catch((err) => console.log(err));
}, []);
```

Now, this empty string([]) being passed to useEffect makes it run only once, and this useEffect function is used to execute it on page load and then to display data, we just need to focus on OCP, like one template and then data is feeded inside it.

```
{ayush.map((sde, idx) => (
  <div className="" key={idx}>
    {ayush.value}
  </div>
))}
```

The mistake that people used to do and repeat is understanding the payload like for eg, we are given a json. So, if it is an object like {} and data is loaded inside it, then it is key value pair and not an array, so we don't need to map the values. Instead, we just have to manually render the values inside the UI.

Now, let's say it is an array like [{}, {}, {}], so first element be like ayush[0].id and to fetch all elements, we use div.

This way, now anybody can build a normal website, one thing to focus on is the cors error, for which once have to whitelist the domain or server with port like http://localhost:3000 or https://ayushmittal.com. So we will take an array of allowed origins as ['http://localhost:3000', 'https://ayushmittal.com'].

So, 
```
app.use(cors({
  origin: ['http://localhost:3000', 'https://ayushmittal.com']
}))
```

This way one can easily build a website. I think nothing is left now, what is left is pagination, filter, sending data in chunks, file streams, buffers, worker threads and many more. Then system design and system architecture also comes into play. After that, security is the major concern too where we need to sign the jwt token with user id and role based payload with an expiry of short term and refresh token with user id based payload with long expiry, which is put inside the cookie, where to authenticate a server, we use authorization bearer token and to execute post and get functionalities and want the data to be displayed, we use credentials: "include" inside the fetch parameters, on every request to include the cookie.

Then comes scalability using messaging queues, why do we need to use it and how the data is produced and consumed and what are different modes involved in its exchange, like direct exchange, topic exchange, fanout exchange and so on. Then comes docker initialisation to create images and their containers to run the servers and so on. The whole image being built to serve the port on which rabbitmq works and then logging and monitoring of the services provided by rabbitmq through docker, its dockerfile to execute node.js commands, etc. are all part defining the whole development, which is never ending and the more we enter into it, the more we are left at the stage where we realise that we know nothing and there is much more to learn and that new zero is the indication of new challenge to solve and grow.
































