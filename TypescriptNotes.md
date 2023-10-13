# Typscript Notes

> These notes explain mostly what makes typscript and javascript different and this these notes are mainly for my own benefit to refer back and to help understand typscript better.

---

### Table of contents

- 1 [Difference between TS vs JS](#difference)
- 2 [Setup](#setup)
  - 2.1[compiling and watching a TS file](#compiling)
  

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



### Strict types in Typescript

Because typescript is scrictly typed it means that typescript doesnt allow us to change variable types once they are defined.

You can define a single type of variable by using the following code:
```ts
let name: string;
let age: number;
let isRegisted: boolean;
```
With this you basically tell typscript you're variable is gonna be of a specific type. whenever you assign a value to this variable typscript can now check if the value matches with the variable type you defined.

### Union types

union types can be used when you expect a value to be of multiple types usually you wanna use this when you expect no more then 2 different types otherwise you're better of using `any` it defeats the purpose of strict types and 

```ts
let unionId: string|number; // The '|' character is used
let unionIds: string|number|boolean; // Multiple union characters can used
```

### The use dynamic types in Typescript
Using special type `any` you can make a variable completely dynamic. This however takes away the concept of typescript using explicit typing is genrally not recommended.
```ts
let dynamic: any;
```


### Type checking in functions

Since typescript is a scrictly types language its necessary to ensure that every variable (also paramenters) are given a type. So to do that with functions you have to write parameters like this: 

```ts
const foo = (bar: number) => { // : and then the type is used the define the type
    return bar++; 
} 
```
Explicit typing like this allows us to type check while we're developing. If types do not match it will give an error and it won't compile the typscript file to javascript.

### Array's and objects

To be added...






