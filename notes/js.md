# JS

## Debuging

```js
debugger; //to set breakpoint
```

### Colorful Console Log

```js
console.log("%c%s","color: red; background: yellow; font-size: 24px;","WARNING!");
```

## Cloning

`const clonedObj= Object.assign({},theobj);`

## SSR vs CSR(Prerendering)

in SSR
(+) SEO
(+) No Client JS Rendering
(-) More Complex and involved build setup
(-) More server side load on Server

# TS

## Loading External Modules

```js
System.defaultJSExtensions=true;
System.import('app')
```