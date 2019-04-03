# CSS

## Mesures

https://sokanacademy.com/blog/19/واحدهای-اندازه‌گیری-در-css-که-شاید-از-وجود-آن‌ها-بی‌خبر-باشید

https://dev.to/nickytonline/which-units-of-measure-do-you-use-and-why-in-css-nf4


## Invert Colors

```css
html {
    -webkit-filter: invert(1.0) hue-rotate(180deg);
    background-color: #000;
    color: #000;
}
```

## Best way of Loading Fonts

* Use WOFF2 Font
* Add `<link rel="preload">`
* Add `@font-face` declaration with `font-display: swap;`