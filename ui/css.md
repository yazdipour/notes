# CSS

- [DOC (Every Web Related Tech)](https://devdocs.io/)
- [tinyjpg](https://tinyjpg.com/)
- [ClipPath Generator](https://bennettfeely.com/clippy/)
- [Sass Cheat Sheet](https://devhints.io/sass)
- [📦Tool to Layout](https://www.layoutit.com/)
- [Material Design Palette Generator](http://mcg.mbitson.com/)
- [HTML, CSS, JS experiments](https://codyhouse.co/library/)
- https://css-tricks.com/
- [SEO Google guidelines](https://varvy.com/)
- [The Ultimate Web Code Generator](https://webcode.tools/)
- [Collection of Links for FrontEnd Developers](http://simurai.com/blog/2014/10/01/front-links)
- [SVG backgrounds](https://www.svgbackgrounds.com)
- [svgeez](https://svgeez.com)

## Frameworks

- https://tailwindcss.com/
- https://primer.style/
- https://www.blazeui.com/

## Dashboard

- [Sexiest Dashboard](http://akveo.com/ngx-admin/#/pages/dashboard)

## Center

```css
.center {
  text-align: center !important;
  align-items: center !important;
  align-self: center !important;
  align-content: center !important;
  justify-items: center !important;
  justify-self: center !important;
  justify-content: center !important;
  place-items: center !important;
  vertical-align: middle !important;
  line-height: 100% !important;
  margin: auto !important;
  position: absolute !important;
  left: 50% !important;
  right: 50% !important;
  transform: translate(-50%, -50%) !important;
}
```

## Grid

[Grid](assets/css/css-grid.png)

## Animation

- http://tobiasahlin.com/spinkit/

## Bootstrap

- [bootstrap4 cheatsheet](https://hackerthemes.com/bootstrap-cheatsheet/)
- https://mdbootstrap.com/
- http://bootstrap.themes.guide
- [Theme builder](https://themestr.app)

## Font

https://fonts2u.com/

## Wordpress

- http://alimir.ir/
- https://includewp.com/

## Mesures

https://sokanacademy.com/blog/19/واحدهای-اندازه‌گیری-در-css-که-شاید-از-وجود-آن‌ها-بی‌خبر-باشید

https://dev.to/nickytonline/which-units-of-measure-do-you-use-and-why-in-css-nf4

## Invert Colors

```css
html {
  -webkit-filter: invert(1) hue-rotate(180deg);
  background-color: #000;
  color: #000;
}
```

## Best way of Loading Fonts

- Use WOFF2 Font
- Add `<link rel="preload">`
- Add `@font-face` declaration with `font-display: swap;`
