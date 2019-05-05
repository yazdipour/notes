# JS

* [Find up to date snippets for common JavaScript use cases](https://codetogo.io/)

## Obfuscator

* http://javascriptobfuscator.com/

## React

* https://nativebase.io/
* https://redux.js.org/
* https://startreact.com/themes/
* https://strapmobile.com/docs/react-native-flat-app-theme/v3.0/overview/introduction

## Cloning

`const clonedObj= Object.assign({},theobj);`

## SSR vs CSR(Prerendering)

in SSR
(+) SEO
(+) No Client JS Rendering
(-) More Complex and involved build setup
(-) More server side load on Server

## TypeScript Loading External Modules

```js
System.defaultJSExtensions=true;
System.import('app')
```

# DevTools

## Colorful Console Log

```js
console.log("%c%s","color: red; background: yellow; font-size: 24px;","WARNING!");
```

## Debuging

```js
debugger; //to set breakpoint
```

## $0 through $4

This very simple feature acts like a history of the selected elements inside the Elements tab. Where, if you use it inside the integrated console you can have fast and direct access to the current element you have selected up to the 5th last element you have selected.

## $_

With $_ you can get the result of the last executed statement without needing any copy and paste.

## monitor()

If you have a function that gets called many times (an event handler for example) and you are not 100% if the arguments it gets passed are correct. Adding a monitor to it would help identify that fairly quickly.

```js
monitor(getDialogue);
getDialogue('main');
console out: "function getDialogue called with arguments: main"
```

## $() and $$()

$() for CSS selector. Use $$() you would like to get all links inside a list. `$$('ul.links a');`