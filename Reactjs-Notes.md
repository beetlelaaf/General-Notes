# React.js Notes

> These notes will cover most of the basics of React (That I've learned so far.)

> NOTE: this file will be **very** prone to change as I am constantly learning new things.

---

### Table of contents

- 1 [Setting up a project](#setup)
  - 1.1 [Tips and Shortcuts](#tips)
  - 1.2 [Passing values between components](#value-passing)
  - 1.3 [Destructuring arrays](#destructure)
- 2 [Routing in react.js](#routing)
  - 2.1 [Adding links to your routing](#linking)
- 3 [Using JSON files as your database](#json)
  - 3.1 [Setting up a json server](#json-server)
  - 3.2 [JSON data structuring](#json-data)
  - 3.3 [Getting the data from the JSON file](#json-fetch)
- 4 [Working with data](#data)
  - 4.1 [Error Handling](#error)
  - 4.2 [Pending Data](#pending)
  - 4.3 [Making a form](#form)
  - 4.4 [Submitting data](#post)
  - 4.5 [Retrieving specific data](#specific)
  - 4.6 [Using Axios instead of Fetch](#axios)
- 5 [Custom Hooks](#hooks)
  - 5.1 [Renaming data](#rename)

---

<div id="setup"></div>

### Setting up a project

Installing node is one of the first steps in the process of creating your react app so make sure you got that intsalled. You can check if you got node installed by simply checking its version with: `Node -v`.

If `npm` is outdated you can use the same command as installing node and then specfying the version of npm you want to install: `npm install -g npm@[version]`.

> If you dont have permission to install npm then use: `sudo npm install -g npm@[version]`

Creating a new react app can be done by using this command `npx create-react-app [Name of the app]`.

Once you've created you react app you're presented with a couple of commands in your terminal that you an use:

`npm start`
Run run you're project in the browser locally.

`npm run build`
Create a build form of your project that can be used once you're putting your app into production.

`npm test`
Run written tests inside your app.

`npm run eject`

**Note:** If everything is installed make sure the `node_modules` folder is referenced in your the `.gitgnore` file. otherwise you would have over 10k unstaged changes from the `node_module` that you dont need to push anyway.

<div id="tips"></div>

### Tips when using react.js

Instead of using classes to define your components, use functions or arrow functions

### Shortcuts (Snippets) to use in react.js

If you want to create a stateless function component use `sfc` and give it a name. The result will look something like this:

```jsx
const MyComponent = () => {
    return (  );
}

export default MyComponent;
```

If you want to create a normal function component use `ffc` and give it a name. The result will look something like this:

```jsx
function MyComponent() {
    return (  );
}

export default MyComponent;
```

<div id="value-passing"></div>

### Passing values between components

we can pass values between components by using the `props`. With props we can pass any value, object or array into another component and use it inside that component. Passing a `prop` into another component can be done like this:

```jsx
// Note That my component, PropName and PropValue can all be custom names like: Banana or Spaceship.
<MyComponent PropName={PropValue} />
```

> NOTE: make sure your naming convention does make sense for both you and others who might want to understand your code.

You now need a parameter inside your component like this:

```jsx
function MyComponent({ PropName }) {}
```

Then we can use this value or object inside our component

<div id="destructure"></div>

### Destructuring arrays (or arrays of objects)

Destructuring an array can be inside a `return` method by using the `map()` function. The map function will assign each object or value inside an array to a variable. You can then use variable in every way you want, for example print it out.
**Note:** Make sure that whenever you use the `map()` inside a `return` method you must put it inside React fragment (`<> </>`) or `<div> </div>`

Inside your map component you need another `return` method. Then write the html you want display along with values that you want to display.
Lastly you want to make sure that your wrapping `div` has a unique `key` associated with them aswell as every child (div) has to have a unique key so that React can keep track of all the components

```jsx
return (
  <>
    {Props.map((prop, index) => {
      return (
        <div key={index}>
          <div key={prop.id}>
            <span>{prop.name}</span>
            <br />
            <span>{prop.content}</span>
          </div>
        </div>
      );
    })}
  </>
);
```

<div id="routing"></div>

### Routing in react.js

To start routing in react you need make use of the `react-router-dom` this module can be installed by running the command: `npm install react-router-dom`
If you want to make sure you're running a stable versipon and not the latest specify the version at the end like this: `npm install react-router-dom@5`

> You can check if you installed your module correctly by checking the `package.json` file

If you want to use the library you need to fisrt import the components you need:

```jsx
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
```

Most of the cases you want your route to be in your `app.js` file. You might also want a navbar most of the time. This is how you make your routes:

```jsx
<BrowserRouter>
  <div className="App">
    <div className="content">
      {/* You dont need this div but it comes if you wanna add other components then is nice to have your routes in a seperate div */}
      <Routes>
        <Route path="/" element={<MyComponent />} />
        <Route path="/secondComponent" element={<MyComponetTwo />} />
      </Routes>
    </div>
  </div>
</BrowserRouter>
```

The `<BrowserRouter>` Will be your main frame for routing. In here you will be able to put routes.
The `<Routs>` Will be the tag that will contain all your individual routes.
The `<Route>` component will be responsible for setting the `path` and the `element` (component) it needs to render once this path is called.

<div id="linking"></div>

#### Adding links to your routing.

Now that we set up our routing its time to make Links that actually use these route.
We can do that by using our navbar and adding links to them.

```jsx
<div className="navbar">
  <Link to={"/"}>
    <button>Home</button>
  </Link>
  <Link to={"/secondComponent"}>
    <button>Second Component</button>
  </Link>
  <Link to={"/otherComponent"}>
    <button>Other Component</button>
  </Link>
</div>
```

Here we intergrate a `button` into every `Link` tag
Inside the `Link` we define the connection to one of the routes we set up. We can do this with the `to` keyword.

Its also possible to wrap a link around a whole `div` so you can make whole components clickable.

```jsx
<Link to={"/SecondComponent"}>
  {" "}
  {/* Link tag that wraps around a div */}
  <div>
    <span>example</span>
    <button>button</button>
  </div>
</Link>
```

<div id="json"></div>

### Using JSON files as our database

If we want to effectively work with a lot of data inside our react app we need a place to `store` that data, aswell as `delete`, `get` and `update` it.
For this we need a database a seperate place for all our data. We can do this in many ways but one were going to use now is to use json files to store our data.

<div id="json-server"></div>

#### Setting up a JSON server

First we need to make a seperate folder inside our react folder which we would call `data` but you can call it whatever you want.
Then we need to make a `.json` file inside that `data` folder. Were going to call it `db.json` which stands for `database`.

Next up, you want to set up a json server using this command: `npx json-server --watch data/db.json --port 8000`

The `--watch` command is used to tell the json server which file to watch so make sure you got the path to your json file right, in this case it will be `data/db.json`
The `--port` command is used to tell the json server which port to run on, this can be any port you like, The default would be port `3000` but since that port is already been used to run our react server we have to specify a different port. in this case we're using port `8000`.

> If you haven't installed all the packages for json-server yet it will ask you to install them, the only thing you have to do is type `y` and then `enter`

After everything has been installed the server will run and you're presented with 1 or 2 links: `Home` and `Resources`.
Your `Home` is just the front page of your json server and shows no data. This is where you land when you have no data inside your json file yet.
Your `Resources` is the place where all your data is stored, the name in the url is the name of one of your sets of data.

<div id="json-data"></div>

#### JSON data structuring

Now that we have got our json server set up, lets add some data to our json file. The first step is to define a `JSON element` we can do that by simply adding `{}` inside here we can define basically enything we want like: `objects`, `arrays`, `strings`, `numbers`, `booleans` and even `null`.
for this example we want to store and array of objects. So the first thing we have define is the `name` of the array, lets say for example: "MyArray" and then we add `[]` to define an array inside our JSON element. the result will look something like this:

```json
{
  "MyArray": []
}
```

Now we want this array to store multiple objects. so we need to define an object by using `{}`. Each object in our array is going to have properties for example an `id` and a `name`. we can define propeties inside an object by first writing the `name` of that property and then a `value` like this: `"id": 2` or `"name": "Jack"`.
If you want to assign multiple properties to an objects then you have to use a `,` at the end of each property you define.
Your JSON file will now look something like this:

```json
{
  "MyArray": [
    {
      "Name": "Jack",
      "id": 1
    }
  ]
}
```

Now we have an array with one object in it. but maybe we want to have multiple object inside the array each with their own name and id.
We can easily do that by adding a `,` at the end of each object and then just add another object the same we did with the first object.

```json
{
  "MyArray": [
    {
      "Name": "Jack",
      "id": 1
    },

    {
      "Name": "Tom",
      "id": 2
    }
  ]
}
```

And we can basically keep doing this forever. Just adding more and more objects to that array.
Now you can also do this with the array, Adding multiple arrays with different data in it.

```json
{
  "MyArray": [
    {
      "Name": "Jack",
      "id": 1
    },

    {
      "Name": "Tom",
      "id": 2
    }
  ],

  "MySecondArray": [
    {
      "apples": true,
      "id": 1
    },

    {
      "apples": false,
      "id": 2
    }
  ]
}
```

To learn more about json check out the [official docs](https://www.json.org/json-en.html)

<div id="json-fetch"></div>

#### Getting the data from the JSON file

Back into our react app we can get the data basically anywhere we want to. To get the data we want we have to make a `get` request to the server.
We can make a request by using the `fetch()` function. Inside that fetch function we put the address to our server along with the data we want to retrieve `http://localhost:8000/myArray`. then we want to add 2 a `.then` function with one of them being for the response of the server and the other the actual data we request.

```jsx
const [data, setdata] = useState(null);

fetch("http://localhost:8000/myArray")
  .then((res) => {
    return res.json();
  })
  .then((data) => {
    setData(data);
  });
```

The first `.then` is responsible to wait for a repsonse from the json server, once there is a response it will return the json from that server.
The second `.then` is responsible for actually getting the data and then we can decide what do do with it. so in this case we will set a `useState()` hook with it that we define on the top. More on `useState()` hooks can be found here: [Using the State Hook](https://reactjs.org/docs/hooks-state.html)

<div id="data"></div>

### Working with data

Now that we have set up a way to get data, We need some form of error handling that can tell us if something is wrong. We also need to know whether data is actually being loaded or not, So we need to tell the user whats going on. Eventually we also want to store data inside the database.

<div id="error"></div>

#### Error Handling

We can add error hadnling bay simply adding a `.catch` function at the bottom of out `fetch` function, and then logging that error to the console.

```jsx
fetch("http://localhost:8000/myArray")
  .then((res) => {
    return res.json();
  })
  .then((data) => {
    setData(data);
  })
  .catch((err) => {
    console.log(err);
  });
```

If we want to let the user know that an error had occured we need to show some text telling what the error. We can do that by setting a variable with the catched error. Next we need to use that variable to display an error to the screen. We display the error message based on if its set or not.

```jsx
const [error, setError] = useState(null);

    .catch(err => {
        setError(err.message); // were setting the variable to be the message of the error since the catch function returns an object.
    })
```

```jsx
{
  error && ( // Inside our render component we check if the variable error is set and if that is true then we display the html inside.
    <div>
      <span>{error}</span>
    </div>
  );
}
```

<div id="pending"></div>

#### Pending Data

If the server needs to bring a lot of data from somewhere or the connection to the server is slow, loading data is going to take some time.
we need a way to tell the user that data is loading instead of letting them stare at an empty screen. We can do that by making another variable just like the error variable and setting that variable to `false`. then we want to set that variable to `true` whenever were fetching data, and then back to `false` whenever were done fetching out data.

```jsx
const [isPending, setIsPending] = useState(false); // The default value of this variable is false since were not fetching any data yet.

fetch("http://localhost:8000/myArray")
    isPending(true); // Whenever the fetch method is called we set the pending to true
    .then(res =>  {
        return res.json();
    })
    .then(data => {
        setData(data);
        setIsPending(false); // Whenever we're done fetching, we can set this variable back to false.
    })
    .catch(err => {
        setError(err.message);
        setIsPending(false); // Also if we experience an error we need to set this variable to false since were not fetching anymore.
    })
```

We can then use the state of that variable to display a message just like the error message.

```jsx
{
  isPending && ( //Check if isPending is true.
    <div>
      <span>Loading data...</span>
    </div>
  );
}
```

> If you want to replicate the effect of data that is loading put your fetch method inside a `timeout` function and set isPending to true before that.

<div id="form"></div>

#### Making a form

To store user data inside out database we need to make a post request to the database. but first we need to make a form where the user can fill in the necessary data.

we'll start by making a `form` that will have an `onSubmit()` function that will trigger the `handleSubmit` function we later define ourselves. then we'll define 2 `input` and one `textarea` which we will give a `placeholder` so we dont need labels. We will aslo make our inputs `required` so we dont have empty data. We will set a `value` to be variable we will also define ourselves and we'll use to get the value of the input. lastly we will give each input an `onChange` property which will be an arrow function calling the corresponding `state` variable. The variable will be set with the `value` of the `event` `target`, which in this case is the `input` itself.

At the bottom we'll add a button. This button will show only if there is no fetch call. If there is a fetch call pending will be true and a loading messages is shown.

```jsx
<form onSubmit={handleSubmit}>
  <input
    type="text"
    placeholder="Title"
    required
    value={title}
    onChange={(e) => setTitle(e.target.value)}
  ></input>

  <input
    type="text"
    placeholder="Author"
    required
    onChange={(e) => setAuthor(e.target.value)}
  ></input>

  <textarea
    rows="10"
    placeholder="Start writing your blog here..."
    required
    onChange={(e) => setBody(e.target.value)}
  ></textarea>

  {!isPending && ( // If there is nothing fetching show a submit button
    <button type="submit">Add Blog</button>
  )}

  {isPending && ( // If there already is something fetching show a loading message.
    <span>Loading...</span>
  )}
</form>
```

<div id="post"></div>

#### Submitting data

No that we got our form setup we only need to send the data to the database and tell it to store that data. Let's first set up our state variables that we specified in the form.

```jsx
const [title, setTitle] = useState("");
const [author, setAuthor] = useState("");
const [body, setBody] = useState("");
const [isPending, setIsPending] = useState(false);
// note how we also need another pending variable to determine to change our button to a loading message.
```

Next, we'll define our `handleSubmit()` function. inside this function we want to make a call

```jsx
function handleSubmit(e) {
  e.preventDefault(); // Prevent the event from performing its default procedure.
  const blog = { title, author, body }; // Make an object that will include the 3 user inputs (can also be an array)

  setIsPending(true); // Set pending to true as were about to send out data to the database
  fetch("http://localhost:8000/blogs", {
    // Make a fetch call to the database
    method: "POST", // Here were telling the database that we want to POST data (Send data)
    headers: { "Content-Type": "application/json" }, // Here were defining its about JSON data.
    body: JSON.stringify(blog), // We send the actual data in JSON format.
  }).then(() => {
    console.log("new blog added"); // This is optional but this way you can check if the process was successful.
  });
  setIsPending(false); // Set pending back to false as the process has been fully completed.
}
```

<div id="specific"></div>

#### Retrieving specific data

Whenever we want to get only one specific object from a list of object we need send a get request with a specific `id` this can be done by including that id in the url so for example: `localhost/blogs/1` where 1 would be the id of the object.

```jsx
<Link to={`/objects/${object.id}`}></Link>
```

To get specific data from the database you most likely have already run a get command to `get` all the data from the database first. Then with that data you can use the `id` of any object of choice to get all the data spicific to that id.

<div id="axios"></div>

<div id="hooks"></div>

### Custom hooks

Throughout our application we might want to make multiple `get` requests from different components. Right now we got one component that has a fucntion which makes a get request, if we got another component that wants to make a `get` request as well it need to have its own function, and make the same call. So this means were basically coding the same function in every component that we want to make a `get` request in.

It would be better if we got one function in a seperate file that makes a get request with any url as `input` and gives up the corresponding data as `output`. This way we can use call this function in any component anytime we want. This is called a `Custom Hook`

We can use a custom hook in this example to make get requests anywhere in our application by simply calling: `usefetch()`

```jsx
import { useState, useEffect } from "react";

const useFetch = (url) => {
  const [data, setData] = useState(null); // To store the data.
  const [isPending, setIsPending] = useState(true); // To store whether the fetch fucntion is waiting for data.
  const [error, setError] = useState(null); // To store the error message.

  useEffect(() => {
    // activate every time this component is rendered.
    fetch(url) // Make a get request to the Json Data file.
      .then((res) => {
        // Check for response
        return res.json(); // Return the json of that response
      })
      .then((data) => {
        // If data is in that response.
        setData(data); // Set data with the retrieved data.
        setIsPending(false); // Set pending to false since the data is loaded.
        setError(null); // Set error to null since there is no error.
      })
      .catch((err) => {
        // If an error occurs then set then catch it.
        setIsPending(false); // Set pending to false since there is an error that occured.
        setError(err.message); // Set error with the message of that error.
      });
  }, [url]);

  return { data, isPending, error }; // Return all the data into an object.
};

export default useFetch;
```

Now with this file called `usefetch.jsx` we can import this in the component we want to it in and then simply call the function.

```jsx
// Here we import the useFetch() function from the file useFetch.jsx.
import useFetch from "useFetch";

// Then anywhere in our code before the Render() function we can call this function and set the variables that it returns.
const { data, isPending, error } = useFetch("http://localhost:8000/blogs");
```

#### Using Axios instead of Fetch

There are multiple ways to make a request to the database. Since I recently started using axios to make requests I added this extra chapter in which ill show you how to make `GET` and `POST` requests.

```jsx
import axios from 'axios';
import { useState, useEffect} from 'react';

/*
  envUrl: is the BaseURL which is static.
  method: is the method we want to use like GET POST DELETE UPDATE.
  url: specifies table we want to get data from.
  body: this is data that we have to give the database whenever we use the POST or UPDATE method to store data
  or update data with new data.
*/

const useAxios = (envUrl, method, url, body) => {

    const [data, setData] = useState(null); // To store the data.
    const [isPending, setIsPending] = useState(true); // To store whether the fetch fucntion is waiting for data.
    const [error, setError] = useState(null); // To store the error message.

    useEffect(() => {
      if(envUrl) {
        axios({baseURL: envUrl, method: method, url: url, data: body})
        .then(res => {
          setData(res.data);
          setIsPending(false);
        })
        .catch(error => {
          setError(error.message);
          }
          setIsPending(false);
        })
      } else {
        setError("No Url");
        setIsPending(false);
      }
    }, [envUrl])

    return {data, isPending, error} // Return all the data into an object.
}

export default useAxios;

// In other component
const {data: blogs, isPending, error} = useFetch(envUrl, "GET", "/users", {});
```

<div id="rename"></div>

#### Renaming data

Whenever we use a custom hook to retrievw data from the database, we always get back an object with `data` in it. Its good practice to name your data so that we and other developers tht read our code know what kind of data it is that were requesting.
We can rename data that we get from our custom hooks like this.

```jsx
// Here we rename the incoming data from our custom hook to be called 'blogs'
const {
  data: blog,
  isPending,
  error,
} = useFetch("http://localhost:8000/blogs");
```
