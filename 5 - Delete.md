# Delete User

This feature will require two routes: 1 for displaying the Delete User page, and another for handling the Delete User form submission.

## Delete User page

```
method          GET
path            /users/:id/delete
route           routes/users.js
view            users/delete.ejs
```

Add the method below to `router.route('/:id/delete')` in `routes/users.js`:

```js
.get(function(req, res){
  knex('users')
    .select('id', 'username')
    .where({
      id: req.params.id
    })
    .first()
    .then(function(user){
      res.render('users/delete', {
        user
      });
    });
})
```

Add the view below to `users/delete.ejs`:

```html
<h1>Delete User</h1>
<form action="/users/<%= user.id %>?_method=DELETE" method="POST">
  <p>Are you sure you want to delete <%= user.username %>?</p>
  <input type="submit" name="Delete User" />
</form>
```

## Delete User form submission

```
method          DELETE
path            /users/:id
route           routes/users.js
```

Add the method below to `router.route('/:id')` in `routes/users.js`:

```js
.delete(function(req, res){
  knex('users')
    .del()
    .where({
      id: req.params.id
    })
    .then(function() {
      res.redirect(`/users`);
    });
})
```
