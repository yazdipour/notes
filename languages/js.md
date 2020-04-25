# JS

- [Recom Plugins](https://twitter.com/hunter1371/status/1253957347648704512)
- [JavaScript benchmarks](https://perf.link/)
- [Find up to date snippets for common JavaScript use cases](https://codetogo.io/)
- [Obfuscator](http://javascriptobfuscator.com/)

## JSON

```js
JSON.stringify(obj);
JSON.parse(str);
```

## Date

- `new Date().toLocaleString("fa-IR-ca-persian")`
- https://date-fns.org/

## Cloning

`const clonedObj= Object.assign({},theobj);`

## SSR vs CSR(Prerendering)

in SSR
(+) SEO
(+) No Client JS Rendering
(-) More Complex and involved build setup
(-) More server side load on Server

## Var, Let, and Const

- `var` variables can be updated and re-declared within its scope; `let` variables can be updated but not re-declared; c`onst variables can neither be updated nor re-declared.
- While `var` and `let` can be declared without being initialised, `const` must be initialised during declaration.

`var` - OldWay :The scope is global when a var variable is declared outside a function. This means that any variable that is declared with var outside a function block is available for use in the whole window.

`let`: Unlikevar, a let variable cannot be re-declared within its scope.

```js
// ok
let greeting = "say Hi";
greeting = "say Hello instead";

//this will return an error.
let greeting = "say Hi";
let greeting = "say Hello instead"; //error: Identifier 'greeting' has already been declared
```

`Const`:

- Variables declared with the const maintain constant values.
- const cannot be updated or re-declared

## TypeScript Loading External Modules

```js
System.defaultJSExtensions = true;
System.import("app");
```

# DevTools

## Table

`console.table(arrayOfArrays)`

![console.table](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/array-of-arrays.png?sfvrsn=fcc7ba3_1)

## Colorful Console Log

```js
console.log(
  "%c%s",
  "color: red; background: yellow; font-size: 24px;",
  "WARNING!"
);
```

## Debuging

```js
debugger; //to set breakpoint
```

## $0 through $4

This very simple feature acts like a history of the selected elements inside the Elements tab. Where, if you use it inside the integrated console you can have fast and direct access to the current element you have selected up to the 5th last element you have selected.

## \$\_

With \$\_ you can get the result of the last executed statement without needing any copy and paste.

## monitor()

If you have a function that gets called many times (an event handler for example) and you are not 100% if the arguments it gets passed are correct. Adding a monitor to it would help identify that fairly quickly.

```js
monitor(getDialogue);
getDialogue('main');
console out: "function getDialogue called with arguments: main"
```

## $() and $\$()

$() for CSS selector. Use $\$() you would like to get all links inside a list. `$$('ul.links a');`
