# Markdown

## Reference

```markdown
![img][logo]
[link][logo]
[logo]: https://github.com/icon48.png "Logo"
```

## Img Size

```markdown
> ![](./pic/pic1s.png =250x)
> ![](./pic/pic1_50.png =100x20)
> <img src="drawing.jpg" alt="drawing" width="200"/>
> ![drawing](drawing.jpg){ width=50% }
```

## Css

```markdown
![pic][logo]{.classname}
[logo]: (picurl)
<style type="text/css">
    .classname{
        width: 200px;
    }
</style>
```

## Expandable/Collapsible

```html
<details><summary>CLICK ME</summary>
<p>

#### yes, even hidden code blocks!

</p>
</details>
```

## Make things Centered

`<p align="center">`