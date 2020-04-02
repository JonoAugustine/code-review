# Code Review

Starting from the entry file and moving down its dependencies,
we have `server.js`.

`server.js`

The entry file initializes an Express server, configures
it to use express encoding & parsing, passport auth middleware,
and api & html routes. This file depends on the `express`
and `express-session` packages to initialize
the server and serve the static data, the `config/passport`, `routes/html-routes`, `routes/api-routes`, and `models` modules.

`config/passport`

  This file configures passport to use a local strategy
  (username/email + password), validating logins against the user's
  password in SQL. This file depends on the `passport` and `passport-local`
  packages and `models` module.

`models/index`

This file loads the `config.json` information to initialize Sequalize.
It depends on the `fs`, `path`, and `sequalize` packages along with the
`/config/config.json` file.

`models/user`

This file defines the User sequalize model and depends on the `bcrypt` package.

`routes/html-routes`

This file defines the route handlers for the signup, login, and members
frontend pages. It depends on the `path` package and the `isAuthenticated`
middleware file.

`config/middleware/isAuthenticated`

This file defines a single express middleware function which redirects
unathenticated clients to the login page.

`routes/api-routes`

This file defines the api route handlers for loging users in and out,
registering new users, and getting user data. This file depends on
the `models` and `config/passport` modules.

Now moving to the public, static files.

`public/login.html`

Provides a simple login page and depends on the `public/js/login`
and `public/stylesheets/style.css` files.

`public/js/login`

This file gives function to the login page and makes API calls to log the
client in.

`public/stylesheets/style.css`

Defines a top margin for the login and signup forms.

`public/members.html`

Shows The name of the currently logged in user. Depends on
`public/stylesheets/style.css` and `public/js/members` files.

`public/js/members`

Gets the logged in user's email from the API and displays it in the
`member-name` span.

`public/signup.html`

Provides a simple login page and depends on the `public/js/signup`
and `public/stylesheets/style.css` files.

`public/js/signup`

Connects the signup html form to the API making a request to create a new user.