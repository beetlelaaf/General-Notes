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


### Type checking in functions

Since typescript is a scrictly types language its necessary to ensure that every variable (also paramenters) are given a type. So to do that with functions you have to write parameters like this: 

```ts
const circ = (diameter: number) => { // : and then the type is used the define the type
    return diameter++; 
} 
```
