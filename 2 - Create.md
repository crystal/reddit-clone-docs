# Create User

This feature will require two routes: 1 for displaying the New User page, and another for handling the New User form submission.

## New User page

```
method          GET
path            /users/new
route           routes/users.js
view            users/new.ejs
```

Add the method below to `router.route('/new')`:

```js
.get(function(req, res){
  res.render('users/new');
});
```

Add the HTML below to `users/new.ejs`:

```html
<h1>New User Page</h1>
<form action="/users" method="POST">
  <label>Full Name:</label>
  <input type="text" name="user[full_name]" autofocus required />
  <label>Username:</label>
  <input type="text" name="user[username]" required />
  <label>Image Url:</label>
  <input type="text" name="user[img_url]" />
  <input type="submit" value="Create New User" />
</form>
```

## New User form submission:

```
method          POST
path            /users
route           routes/users.js
```

Add the method below to `router.route('/')`:

```js
.post(function(req, res){
  knex('users')
    .insert({
      full_name: req.body.user.full_name,
      username: req.body.user.username,
      img_url: req.body.user.img_url
    })
    .returning('id')
    .then(function(id) {
      res.redirect(`/users/${id}`);
    });
})
```
