# Read (All) Users

This will render a page that displays all users.

```
method          GET
path            /users
route           routes/users.js
view            users/index.ejs
```

Add the method below to `router.route('/')` in `routes/users.js`:

```js
.get(function(req, res){
  knex('users')
    .select('id', 'username')
    .then(function(users){
      res.render('users/index', {
        users
      });
    });
})
```

```html
<h1>All Users</h1>
<ul>
  <% users.forEach(function(user){ %>
     <li><%= user.username %> <a href="/users/<%= user.id %>">View</a> <a href="/users/<%= user.id %>/edit">Edit</a> <a href="/users/<%= user.id %>/delete">Delete</a></li>
  <% }); %>
</ul>
```

# Read (One) User

This will render a page that displays a single user.

```
method          GET
path            /users/:id
route           routes/users.js
view            users/show.ejs
```

Add the method below to `router.route('/:id')` in `routes/users.js`:

```js
.get(function(req, res){
  knex('users')
    .select('id', 'username', 'full_name', 'img_url')
    .where({ id: req.params.id })
    .first()
    .then(function(user) {
      res.render('users/show', {
        user
      });
    });
})
```

Add the HTML below to `users/index.ejs`:

```html
<h1><%= user.username %></h1>
<ul>
    <li>Full Name: <%= user.full_name %></li>
    <li>Image URL: <%= user.img_url %></li>
    <li><a href="/users/<%= user.id %>/edit">Edit user</a></li>
</ul>
```
