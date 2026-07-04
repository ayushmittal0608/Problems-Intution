# ORM (Object Relational Mapper)
It is a layer that sits between our application code and SQL database. So, instead of writing raw SQL queries, we can just work with TS objects and methods and ORM converts them into SQL.

Now, for eg, someone has asked to build some application and they want us to deliver it fast with utmost efficiency and better code design for clarity, then we don't have to write manual SQL queries, and it becomes easy for us to refactor tables or columns, also it helps us preventing major SQL injection problems.

So, ORM is the best way to build production ready applications with type safety, protection against SQL injections and table or column refactoring with flexibility to migrate. So, for achieving it, I use drizzle ORM as it boosts up the efficiency of a developer and the most advantageous thing that it offers is the ease of learning.

Through this, we just need to define the schema of a table and the whole table is being generated, migrated and pushed through CLI commands, where we can even push the changes that we need with or without truncating the whole table.

The best feature it provides is that whenever we generate a migration, we get an SQL file inside our out folder, with anonymous names where it is written that what migration we gonna perform. Then as per the SQL migrations file generated in drizzle ORM, we can check that if generated migration is really aligning as per the needs and if so, we just apply migrations to have our table ready.

Once, the table is migrated, then we can perform push operation for any changes inside the table. So, now same schema is what we can use to insert queries inside our DB. I think it really improves the overall efficiency of a developer.



