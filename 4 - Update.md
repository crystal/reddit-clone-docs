### Update User

This feature will require two routes: 1 for displaying the Edit User page, and another for handling the Edit User form submission.

## Edit User page

```
method          GET
path            /users/:id/edit
route           routes/users.js
view            users/edit.ejs
```

Add the method below to `router.route('/:id/edit')` in `routes/users.js`:

```js
.get(function(req, res){
  knex('users')
    .select('id', 'username', 'full_name', 'img_url')
    .where({ id: req.params.id })
    .first()
    .then(function(user) {
      res.render('users/edit', {
        user
      });
    });
})
```

Add the view below to `users/edit.ejs`:

```html
<h1>Edit User Page</h1>
<form action="/users/<%= user.id %>?_method=PUT" method="POST">
  <label>Full Name:</label>
  <input type="text" name="user[full_name]" autofocus required value="<%= user.full_name %>" />
  <label>Username:</label>
  <input type="text" name="user[username]" required value="<%= user.username %>" />
  <label>Image Url:</label>
  <input type="text" name="user[img_url]" value="<%= user.img_url %>" />
  <input type="submit" value="Update User" />
</form>
```

Note: html doesn't support anything other than get & post, which is why this project uses the method_override library. You'll notice above, the PUT method is overridden as a POST method; and the form action includes `?_method=PUT` at the end of the url (i.e `/users/1?_method=PUT`).

## Edit User form submission

```
method          PUT
path            /users/:id
route           routes/users.js
```

Add the method below to `router.route('/:id')` in `routes/users.js`:

```js
.put(function(req, res){
  knex('users')
    .update({
      full_name: req.body.user.full_name,
      username: req.body.user.username,
      img_url: req.body.user.img_url
    })
    .where({
      id: req.params.id
    })
    .returning('id')
    .then(function(id) {
      res.redirect(`/users/${id}`);
    });
})
```
