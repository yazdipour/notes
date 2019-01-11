# CSS

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