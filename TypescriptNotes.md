# Typscript Notes

> These notes explain mostly what makes typscript and javascript different and this these notes are mainly for my own benefit to refer back and to help understand typscript better.

---

### Table of contents

- 1 [Difference between TS vs JS](#difference)
- 2 [Setup](#setup)
  - 2.1[Compiling and watching a TS file](#compiling)
  - 2.3[Configuring public and src folders](#publicsrc)
  - 2.4[Downleveling](#downleveling)
  - 2.5[Strictness of typescript](#strictness)
- 3[The use of dynamic types](#dynamic)
- 4[Explicit types in typescript](#explicittypes)
  - 4.1[Union types](#union)
  - 4.2[Explicit typing with functions](#functions)
  - 4.3[Explicit typing with array's](#arrays)
  - 4.4[Explicit typing with objects](#objects)
  

<div id="difference"></div>

### Difference between TS and JS

Typscript is a superset of javascipt and allows you to do use a strict types, it supports modern features such as arrow function, let, const and a lot of extra features such as Generics, intefaces and tuples, etc.


<div id="setup"></div>

### Setup
Before you can start using typescript you must firsr make sure to install node and then use `nmp install -g typescript`

you check if you have typscript installed by typing `tsc` or if you're using `powershell` type `tsc.cmd` in the terminal and it will show the current version your typsescript compiler.


<div id="compiling"></div>

#### Compiling and watching a TS file

To compile you typescript files to js files use `tsc [filename]` or `tsc.cmd [filname]`. but manually compiling everytime is not recommended so added the `-w` flag (meaning watch) will automatically watch the file and compile on save and changes.

<div id="publicsrc"></div>

### Configuring a public and src folder

As your project starts to scale up you're going to have multiple different typscript files that wilkl be sorted in different folders. To be able to compuile alle the files we need a source folder `src` and a public folder `public`. The `src` folder will contain all the typscript files and the public folder will contain the rest of the websites along with the compiled files.

Once you made a `src` and `public` folder inside the src folder use `tsc.cmd --init` to create a config folder inside the src folder, this folder will allow you to configure everything about your compiler.

One of the things we need to change is the `rootDir` and the `outDir` the root directory tells the compiler where the files are that need to be compiled. the out directory tells the compiler where the compiled files need to be placed. In this case since we made a `public` and a `src` folder were goign to add the following lines: `"rootDir": "./src",` and `"outDir": "./public",`

Since were setting a root directory to point to our `src` folder, the compiler expectes all the root files to be in that `src` folder. Any typescript file that is detected outside of that folder will cause an error we we try to compile it, So we need to tell the compiler to ignore all the files that are detected outside of the `src` folder. We can do that by adding the following line at the bottom of out config file between the 2 curly brackets: `"include": ["src"]`.

Now we can use `tsc.cmd -w` and it will automatically watch only the src folder for changes in the `src` folder and compile them.

<div id="publicsrc"></div>

### Downleveling
By default when compiling TS to JS, typescript will target the lowest version of ES (ECMAScript 2013, ES3) which will turn some things like template strings like this:
```ts
`Hello ${person}, How are you?`;
```
And turn it into this: 
```ts
"Hello ".concat(person, ", How are you?"); 
```
Which you might not want, so if you want to target a higher version like ES5 or ES6 you can do that inside the config file of tsc, by setting `"target":` to `es2015` or higher.

> Note that upgrading to a higher version might not be supported by every browser so keep that in mind.

<div id="strictness"></div>

### Strictness of typescript
By default the stricness of typescript is set to the the maximum meaning it will check basically everything it can, you can however change that in the config file and set only certain things to be checked like for example: `noImplicitAny` or `strictNullChecks`.


<div id="dynamic"></div>

### The use fully dynamic types in Typescript
Using special type `any` you can make a variable completely dynamic. This however takes away the concept of typescript using explicit typing is genrally not recommended.
```ts
let dynamic: any;
```
> The keyword `any` is generally used if you dont want a particular value to cause typechecking errors.

<div id="explicittypes"></div>

### Explicit types in Typescript

Because typescript is scrictly typed it means that typescript doesnt allow us to change variable types once they are defined. By defining a variable explicitly you can prevent a value from ever changing types. This is different from setting a value directly as you dont explicity tell Typescript what type of value its going to be and you basically let Typescript figure it out himself.

You can define a single type of variable by using the following code:
```ts
let name: string;
let age: number;
let isRegisted: boolean; 
```
> Always use lowercase when defining `string`, `number` and `boolean`

> Notice how Typescript doesnt use `float` and `int` seperatly but instead uses `number` to represent any number regardless if its a interger or float.

With this you basically tell typscript you're variable is gonna be of a specific type. whenever you assign a value to this variable typscript can now check if the value matches with the variable type you defined.

<div id="union"></div>

### Union types

union types can be used when you expect a value to be of multiple types usually you wanna use this when you expect no more then 2 different types otherwise you're better of using `any` it defeats the purpose of strict types and 

```ts
let unionId: string|number; // The '|' character is used
let unionIds: string|number|boolean; // Multiple union characters can used
```

<div id="functions"></div>

### Explicit typing with functions

Since typescript is a scrictly types language its necessary to ensure that every variable (also paramenters) are given a type. So to do that with functions you have to write parameters like this: 

```ts
const foo = (bar: number) => { // : and then the type is used the define the type
    return bar++; 
} 
```
Explicit typing like this allows us to type check while we're developing. If types do not match it will give an error and it won't compile the typscript file to javascript.

<div id="arrays"></div>

### Explicit typing with array's

Array's can also be explicitly typed in many different ways to define the most simple array we can use the follwing code

```ts
let numberArray: number[];
```
To define this variable as an empty array modify the line so it looks like this:

```ts
let numberArray: number[] = [];
```
Union types can also be used with arrays like this this will define an array that can accept both numbers and strings
```ts
let numberAndStringArray: (number|string)[];
```
You can also define you array to either be one of 2 or more different types of arrays.

```ts
let numberOrStringArray: (number[]|string[]);
```

You can even define a variable to be either an array or a single type like this:
```ts
let numberArrayorString: (number[]|string);
```

<div id="objects"></div>

### Explicit typing with objects

To be added...