# React.js Notes

> These notes will cover most of the basics of React (That I've learned so far.)

> NOTE: this file will be **very** prone to change as I am constantly learning new things.

---

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

**Note:** If everything is installed dont forget to put `node_modules` and `package-lock.json` into the `.gitgnore` file. otherwise you would have over 10k unstaged changes from the `node_module` that you dont need to push anyway.


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

### Passing values between components 

we can pass values between components by using the `props`. With props we can pass any value, object or array into another component and use it inside that component. Passing a `prop` into another component can be done like this:
`jsx
// Note That my component, PropName and PropValue can all be custom names like: Banana or Spaceship.
<MyComponent PropName={PropValue}/>
`
> NOTE: make sure your naming convention does make sense for both you and others who might want to understand your code.

You now need a parameter inside your component like this:
`jsx
function MyComponent({PropName}) {}
`
Then we can use this value or object inside our component

### Destructuring arrays (or arrays of objects)

Destructuring an array can be inside a `return` method by using the `map()` function. The map function will assign each object or value inside an array to a variable. You can then use variable in every way you want, for example print it out.
**Note:** Make sure that whenever you use the `map()` inside a `return` method you must put it inside React fragment (`<> </>`) or `<div> </div>`

Inside your map component you need another `return` method. Then write the html you want display along with values that you want to display.
Lastly you want to make sure that your wrapping `div` has a unique `key` associated with them aswell as every child (div) has to have a unique key so that React can keep track of all the components
```jsx
return (
    <>
        {blogs.map((blog, index) => {
            return (
                <div key={index}>
                    <div key={blog.id}>
                        <span>{blog.name}</span><br/>
                        <span>{blog.content}</span>
                    </div>
                </div>
            );
        })}
    </>
);
```

### Routing in react.js

To start routing in react you need make use of the `react-router-dom` this module can be installed by running the command: `npm install react-router-dom`
If you want to make sure you're running a stable versipon and not the latest specify the version at the end like this: `npm install react-router-dom@5`
> You can check if you installed your module correctly by checking the `package.json` file 

If you want to use the library you need to fisrt import the components you need:
`jsx
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
`
Most of the cases you want your route to be in your `app.js` file. You might also want a navbar most of the time. This is how you make your routes:
```jsx
<BrowserRouter>
    <div className="App">
    <div className="content"> 
    {/* You dont need this div but it comes if you wanna add other components then is nice to have your routes in a seperate div */}
        <Routes>
        <Route path='/' element={<Main />}/>
        <Route path='/blogs' element={<BlogList />}/>
        </Routes> 
    </div>
    </div>
</BrowserRouter>
```
The `<BrowserRouter>` Will be your main frame for routing. In here you will be able to put routes.
The `<Routs>` Will be the tag that will contain all your individual routes.
The `<Route>` component will be responsible for setting the `path` and the `element` (component) it needs to render once this path is called.

#### Adding links to your routing.

Now that we set up our routing its time to make Links that actually use these route.
We can do that by using our navbar and adding links to them.
```jsx
<div className="navbar">
    <Link to={'/home'}><button>Home</button></Link>
    <Link to={'/blogs'}><button>Blogs</button></Link>
    <Link to={'/add'}><button>Add blog</button></Link>
    <Link to={'/about'}><button>About</button></Link>
</div>
```

Here we intergrate a `button` into every `Link` tag
Inside the `Link` we define the connection to one of the routes we set up. We can do this with the `to` keyword.

Its also possible to wrap a link around a whole `div` so you can make whole components clickable.

```jsx
<Link to={'/blogs'}> {/* Link tag that wraps around a div */}
    <div>
        <span>example</span>
        <button>button</button>
    </div>
</Link>
```

