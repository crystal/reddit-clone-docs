# What to do about all this CRUD

## Tools

Here are the tools you'll be using:

- `body-parser` - parses request body as JSON
- `ejs` - renders ejs templates to HTML
- `express` - handles backend operations
- `knex` - handles database operations
- `locus` - live debugging via REPL
- `pg` - works with knex to handle database operations
- `method-override` - allows us to work around the html restrictions on delete & put

## Frontend vs Backend

The 2 major tools you'll be using are `express` and `ejs`.

`express` is your backend. It will handle your routing, database and pass data to your `ejs` templates.

`ejs` is your frontend. It will take data from your backend and render HTML based on your ejs templates.

## Routing

Routing is handled by `express`. For this project, we'll split up our routes for our `comments`, `posts` and `users`:

- routes/comments.js (root path: `/users`)
- routes/posts.js (root path: `/posts`)
- routes/users.js (root path: `/users`)

By default, each of these routes has a root path that will be prepended to any routes defined under it (i.e `/:id` in `users.js` will become `/users/:id`).

## View Engine

View Engines enable you to use and render different HTML templates such as ejs, Pug (fka Jade) and Handlebars.

For our project, we are using the `ejs` templating engine to make our HTML dynamic.

To better visualize what `ejs` has to offer, take a look at the code below.

HTML Code:

```
<ul>
  <li>user1</li>
  <li>user2</li>
  <li>user3</li>
</ul>
```

`ejs` Code:

```
<ul>
  <% users.forEach(function(user) { %>
     <li><%= user.username %></li>
  <% }); %>
</ul>
```

Notice that the `HTML` code is static; each user is hard-coded. The `ejs` code, however, allows us to dynamically display users. When new users are added, or if we want to filter users, or if we want to sort users; we can now do it dynamically by passing it into our routes.

Another common pattern in `HTML` templating is making the page title dynamic. Check out the examples below.

HTML Code:

```
<head>
  <title>My Site</title>
</head>
```

`ejs` Code:

```
<head>
  <title><%= title %></title>
</head>
```

### ejs Support in Atom

`ejs` can kinda suck in Atom. The syntax highlighting doesn't work right, so it makes it difficult to know if you're writing the correct syntax. Use Google and this documentation as your guide. You can also install the `language-ejs` package, to help Atom lint your files better.

## Try It Out

In the next sections of this tutorial, we'll add all CRUD methods to our `users` route.
