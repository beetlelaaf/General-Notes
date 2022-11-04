# TailwindCSS Notes

These notes aren't by any means a tutorial its more like a set of barebone ways to make simple website components
These notes change over time and might include a lot of mistakes since im still learnign tailwindCSS so please do not see this as the right way to use tailwindCSS.

---

### Table of contents

- 1 [Intergrating TailwindCSS](#setup)
- 2 [Important classes](#important)
- 3 [Navbar examples](#navbar)
- 4 [Custom animations](#customanimations)

---

<div id="setup"></div>

### Intergrating TailwindCSS

T.B.I

<div id="important"></div>

### Important classes

| Syntax     | Description             | Additional Syntax       | Description                        |
| ---------- | ----------------------- | ----------------------- | ---------------------------------- |
| `p`        | Padding                 | `px` / `py`             | Padding x and y specific           |
| `m`        | Margin                  | `mx` / `my`             | Margin x and y specific            |
| `w`        | Padding left and right  | `w-full`                | Full width                         |
| `h`        | Margin left and right   | `h-full`                | Full height                        |
| `sm:`      | Small screen size       | -                       | -                                  |
| `md:`      | Medium screen size      | -                       | -                                  |
| `lg:`      | Large screen size       | -                       | -                                  |
| `xl:`      | Extra large screen size | `xl2` / `xl3` / `xl4`   | Even larger screen sizes           |
| `bg`       | Background color        | `slate` / `gray`        | Any build in color                 |
| `text`     | Manipulate text         | `white` / `sm` / `left` | Any function that manipulates text |
| `relative` | Position bahavior       | `absolute` / `fixed`    | -                                  |
| `a`        | Position bahavior       | `absolute` / `fixed`    | -                                  |

<div id="navbar"></div>

### Navbar examples

Navbar example using flexbox with logo

```html
<nav className="bg-slate-800 shadow-md shadow-slate-400">
  <div className="mx-auto px-2 sm:px-4 lg:px-5">
    <div className="relative flex h-20 items-center">
      <img src="{logo}" className="h-20 w-20" alt="logo" />
      <div className="h-full grid-cols-5 flex items-center sm:px-1 lg:px-4">
        <a className="mx-3 py-3 px-4 text-white"> Home </a>
        <a className="py-3 px-4 text-white"> About </a>
        <a className="py-3 px-4 text-white"> Dashboard </a>
        <a className="py-3 px-4 text-white"> Admin </a>
        <a className="py-3 px-4 text-white"> Nonsense </a>
      </div>
      <div className="h-full grid-cols-3 flex sm:px-1 lg:px-4 ml-auto">
        <a className="text-white">Icon</a>
        <a className="text-white">Icon</a>
      </div>
    </div>
  </div>
</nav>
```

<div id="customanimations"></div>

### Custom Animations

You can make custom animation by adding the following code inside `tailwind.config.js` inside `theme:`

```jsx
    extend: {
      keyframes: {
        // Here can make your own animations
      },
    },
```

For our first animation we're going to make an animation called wiggle. The wiggle animation will be a simple wiggle from left to right, So first we'll give our animation a name and add the keyframes like this:

```jsx
  theme: {
    extend: {
      keyframes: {
        wiggle: { // Name of the animnation
          "25%": { transform: "rotate(15deg)" }, // The keyframes just like css
          "50%": { transform: "rotate(0deg)" },
          "75%": { transform: "rotate(-15deg)" },
        },
      },
    },
  },
```

Lastly we'll build define the animation as a keyword so that we can use it anywhere in our code.

```jsx
  theme: {
    extend: {
      keyframes: {
        wiggle: {
          "25%": { transform: "rotate(15deg)" },
          "50%": { transform: "rotate(0deg)" },
          "75%": { transform: "rotate(-15deg)" },
        },
      },
      animation: { // here we can define additional behavior like you would with css aswell like duration and linear
        wiggle: "wiggle 0.5s linear",
      },
    },
  },
```

And boom you got yourself a costum animation that you can use anywhere in your code!
