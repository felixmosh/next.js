# Example app utilizing cookie-based authentication

## How to use

### Using `create-next-app`

Download [`create-next-app`](https://github.com/segmentio/create-next-app) to bootstrap the example:

```
npm i -g create-next-app
create-next-app --example with-cookie-auth with-cookie-auth-app
```

### Download manually

Download the example [or clone the repo](https://github.com/zeit/next.js):

```bash
curl https://codeload.github.com/zeit/next.js/tar.gz/canary | tar -xz --strip=2 next.js-canary/examples/with-cookie-auth
cd with-cookie-auth
```

### Run locally

The repository is setup as a [monorepo](https://zeit.co/examples/monorepo/) so you can run start the development server with `now dev` inside the project folder.

Install the packages of `/api` and `/www` using `npm` or `yarn`:

```bash
cd api
npm install
cd ../www
npm install
```

Now you can start the development server in the root folder:

```bash
now dev
```

You can configure the `API_URL` environment variable (defaults to `http://localhost:3000`) with [Now env](https://zeit.co/docs/v2/development/environment-variables/#using-now.json) in the `now.json` file:

```bash
"build": {
  "env": {
    "API_URL": "https://example.com"
  }
},
```

### Deploy

Deploy it to the cloud with [now](https://zeit.co/now) ([download](https://zeit.co/download))

```bash
now
```

## The idea behind the example

In this example, we authenticate users and store a token in a cookie. The example only shows how the user session works, keeping a user logged in between pages.

This example is backend agnostic and uses [isomorphic-unfetch](https://www.npmjs.com/package/isomorphic-unfetch) to do the API calls on the client and the server.

The repo includes a minimal passwordless backend built with [Micro](https://www.npmjs.com/package/micro) that logs the user in with a GitHub username and saves the user id from the API call as token.

Session is synchronized across tabs. If you logout your session gets logged out on all the windows as well. We use the HOC `withAuthSync` for this.

The helper function `auth` helps to retrieve the token across pages and redirects the user if not token was found.
