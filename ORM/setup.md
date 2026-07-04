# Setup

1. Dependency Setup
```
npm install drizzle-orm postgres
npm installl -D drizzle-kit tsx
```

2. Create .env
We set env variables for accessing our psql database.
```
DATABASE_URL=postgres://<username>:<password>@localhost:5432/<DB_Name>
```
So, as per the URL, we can note that postgres is not running over https but over postgres with our username and password to be hosted at localhost and being connected at port 5432. Since we are having n number of DBs inside a single user credentials, we have our DBs over the routes to the URL.

3. Configure Drizzle
```
import { defineConfig } from "drizzle-kit";
export default defineConfig({
    schema: "./src/db/schema.ts",
    out: "./drizzle",
    dialect: "postgresql",
    dbCredentials: {
        url: process.env.DATABASE_URL!,
    },
});
```
So, now here, we have defined the whole pSQL config taking a part of drizzle-kit where we are defining the config. Now, there is a difference between {} and simple file name which is that here, we are using a part or a functionality or a component of drizzle-kit, not the whole module.

So, now we define our schema location, output location, dialect/language and most importantly db credentials where we pass the URL for allowing drizzle-kit to access it.

4. Create Schema
```
import { pgTable, serial, text, integer } from "drizzle-orm/pg-core";

export const users = pgTable("users", {
    id: serial("id").primaryKey(),
    username: text("username").notNull(),
    email: text("email").notNull(),
    age: integer("age")
});
```

5. Connect Database
```
import postgres from "postgres";
import { drizzle } from "drizzle-orm/postgres-js";

const client = postgres(process.env.DATABASE_URL!);

export const db = drizzle(client);
```

Now, since we want to connect our drizzle ORM with postgres, we will define a setup configuration to connect, where we import whole postgres and drizzle component from drizzle-orm/postgres-js and then take a client constant to store postgres db credentials in order to pass them to drizzle and exporting it everywhere inside our schema and the files we use, which varies as per the architecture taken and most of the time, it resides within the services part of our node.js backend.

I think once it is being setup, it becomes easy to implement the different architectural models based on our preferences that at what scale, we want to take our application.

For someone who has started learning it thinks about how complex the system will be that the other person have to write too many lines of code and run the application but what really matters is what architectural decision we want to take to make our code better.

For eg, we are setting up a server running at some port, then we design different routes file and connect it to server port side, and then add controller for controlling different routes, for eg, for a single crud operation, we want post, get, getById, update, delete and so on, then inside the controller is where everything is being implemented like in a single post, what we need to do, what actions do we need to perform inside service part where we are inserting using drizzle ORM.

I think we should not discuss all of it here and slowly and gradually, learn about each and everything to make software engineering way more easier and simpler so that we could spend most of the time solving more complex and unheard problems, rather than sticking to this part only.

I know it is a time where AI has come which solves most of the problem and maybe we can't have the knowledge that AI has, also there is a major hype within the people who are just taking AI courses, learning AI but foundation of building AI can only come when we start believing that software engineering has become a way more easier and we have tried all of the complexities and architectures in our life and finally get to the stage where we need to shift to probablistic model.

That urge to think a way forward in deterministic system to move to probablistic model and thinking about how users interact at a massive scale where each and every content is relevant, there we need to segregate it based on behavioural analysis, machine learning and AI.

So, it is well-said that a monument has been built on junkyard where getting money through AI courses and learning AI can be demolished and what can survive would be a strong hold over software engineering which is the base foundation to build a stable and long lasting monument. This is today's knowledge from my side which is not as smart as the other people learning AI and taking AI courses to earn well.
