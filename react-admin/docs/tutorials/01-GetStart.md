# Setting Up

React-admin uses React. We’ll use [Vite](https://vitejs.dev/) to create an empty React app, and install the `react-admin` package:
```sh
yarn create vite test-admin --template react-ts
cd test-admin/
yarn add react-admin ra-data-json-server
yarn dev
```

You should be up and running with an empty React application on port `5173`.

> Although this tutorial uses a TypeScript template, you can use react-admin with JavaScript if you prefer. Also, you can use `create-react-app`, `Next.js`, `Remix`, or any other React framework to create your admin app. React-admin is framework-agnostic.

# Using an API As Data Source
React-admin runs in the browser, and fetches data from an API.

We’ll be using [JSONPlaceholder](https://jsonplaceholder.typicode.com/), a fake REST API designed for testing and prototyping, as the data source for the application.

JSONPlaceholder provides endpoints for users, posts, and comments. The admin we’ll build should allow to Create, Retrieve, Update, and Delete (CRUD) these resources.

# Making Contact With The API Using a Data Provider

Bootstrap the admin app by replacing the `src/App.tsx` by the following code:

```TypeScript
// in src/App.tsx
import { Admin } from "react-admin";
import jsonServerProvider from "ra-data-json-server";

const dataProvider = jsonServerProvider('https://jsonplaceholder.typicode.com');

const App = () => <Admin dataProvider={dataProvider} />;

export default App;
```
```css
/* in src/index.css */
body {
    margin: 0;
}
```

Lastly, add the `Roboto` font to the `index.html` file:
```html
<!-- in ./index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Admin</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

> You can also install the `Roboto` font locally by following the instructions from the [MUI starter guide](https://mui.com/material-ui/getting-started/installation/#roboto-font).

# Mapping API Endpoints With Resources
```diff
// in src/App.tsx
-import { Admin } from "react-admin";
+import { Admin, Resource, ListGuesser } from "react-admin";
import jsonServerProvider from "ra-data-json-server";

const dataProvider = jsonServerProvider('https://jsonplaceholder.typicode.com');

-const App = () => <Admin dataProvider={dataProvider} />;
+const App = () => (
+ <Admin dataProvider={dataProvider}>
+   <Resource name="users" list={ListGuesser} />
+ </Admin>
+);

export default App;
```