# PrismaORM

## Table of Contents
- [PrismaORM](#prismaorm)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Installing Prisma](#installing-prisma)
  - [Schema and Models](#schema-and-models)
    - [Database Introspection](#database-introspection)
  - [Migrations](#migrations)
  - [Using Prisma](#using-prisma)

## Introduction 

While SQL is an essential skill for any serious backend developer, in many projects one might be inclined to disregard the humble SQL driver for an ORM, or Object Relational Mapper. Using relational database terms, ORMs essentially treat database tables as types, and rows in tables as individual objects so that they're easily accessed by developers, who no longer have to write queries themselves. Instead, the ORM package itself generates and run the queries when the developer calls ORM functions. This approach comes with several advantages, such as safety, simplicity, and database management system agnosticism, however be warned that certain advanced database features may be unavailable and for highly complex/specific queries you're still better off writing them yourself.

PrismaORM is an ORM for JavaScript and TypeScript meant to streamline backline development with a suite of convenient features. In this guide we'll go through the basics of setting up Prisma and using it.

## Installing Prisma 

You install Prisma like any npm package, in your (preferably) TypeScript project run
```
npm install prisma --save-dev
```
To install the package. Then run 
```
npx prisma init --datasource-provider sqlite
```
To set up prisma to use sqlite. Don't worry, you can always change the datasource later to point towards the database you intend to use. 

## Schema and Models 

Now you should be greeted with a new `prisma` directory in your project folder. Within this directory you'll find a `migration` folder and a `schema.prisma` file. The `migration` folder is where Prisma will store its migration history, and `schema.prisma` is where you'll do all your modelling.

Prisma uses its own syntax, which I personally found pretty intuitive to learn. 

In the following example I declare two models, User and Post.

```
model User {
    id      Int     @id @default(autoincrement())
    email   String  @unique
    name    String?
    posts   Post[]
}
```
```
model Post {
    id          Int     @id @default(autoincrement())
    title       String
    content     String?
    published   Boolean @default(false)
    author      User    @relation(fields: [authorId], references: [id])
    authorId    Int
}
```
These two examples show the most important features of a model description. 

`User` and `Post` are the names of tables; `id`, `email`, `name` are `User`'s fields or columns. `User` and `Post` have a many-to-one relationship defined by the `posts` field in `User` and the foreign key field `author` on `Post`. Next to the types of the fields starting with '@' are decorators, which you can use to define behaviour.

Database modelling is an art, and there is much that we're not covering, but this should give you an idea of what to expect. 

### Database Introspection

What if you already have a database, and you want to start using Prisma with your tables already defined? With Prisma, you can `introspect` your database and automatically generate a schema file based on the current state of your tables.

Once you set up your Prisma client to properly connect with your database, simply run 
```
npx prisma db pull
```
To update your schema file. Be warned that as with any automatically generated code, you might have to do a lot of renaming and refactoring for the schema to be legible.

## Migrations

Once your models are setup, you'll need to make sure that the actual state of your database reflects the models in your schema file. 

You should run
```
npx prisma migrate dev --name init
```
To create your initial migration, when you're developing your backend you might need to make many changes to your database, and for that you should use `npx prisma db push`, but to do that you'll have to set up what's called a shadow database and that's a whole new can of worms so we won't go into that just yet. 

Behind the scenes, the migrate command also ran `npx prisma generate`, which builds the JavaScript package you'll use to interact with your database and access nice features like autocompletion and type safety.

## Using Prisma

Now that you've done all the hardwork of setting up Prisma, here's your chance to actually use it. Let me just emphasize right here that Prisma is a backend only library. You can't run it client side, if you're calling calling the Prisma client in any code that will be served frontend it just won't work! 

In any case, for this quickstart let's assume you're just writing a node script. Let's create a script file with this being the content:
```js
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

async function main() {
    ...
}

main()
    .then(async () => {
        await prisma.$disconnect()
    })
    .catch(async (e) => {
        console.error(e)
        await prisma.$disconnect()
        process.exit(1)
    })
```
What you need to know is that the `prisma` variable is where you're going to call all the prisma functions, and the bit at the end is just some boiler plate to ensure that you're not inhaling all of your database's available connections. 

The way the prisma client works is that all the query logic and data is expressed through a (heavily) nested JavaScript object. 

here is an example of how to create a new `User` record. 

```js
...
async function main() {
    const user = await prisma.user.create({
        data: {
            name: 'Matthew',
            email: 'Matthew@utoronto.ca',
        }
    })
}
...
```
Getting all `User` records that has an email address with the domain 'utoronto.ca' and the name Matthew with their `Post`s included is the following:
```js
...
async function main() {
    const users = await prisma.user.findMany({
        where: {
            email: {
                endsWith: 'utoronto.ca',
            },
            name: 'Matthew',
        },
        include: {
            posts: true,
        }
    })
}
...
```

And so on, you get the gist. The most difficult part of Prisma is learning these functions. But in my experience they're pretty intuitive and you'll pick up on them much faster than SQL.

This concludes this short quickstart, Prisma is a very useful library that's still under active development, I enjoyed using it for my projects and I encourage you to check it out as well. The [Prisma Documentation](https://www.prisma.io/docs) explains all of this better than I ever could. Good luck coding. 