# ASP

## Razor

With Razor

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_39360205.png)

Without Razor

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_7AB0B45E.png)

### @{ code } Multi-line Statements

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_4B321FC5.png)

### @( code ) Multi-Token Statements

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_75321DED.png)

### Layout/Master Page Scenarios

#### Layout Page

`Layout.cshtml`

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_6D0A0A24.png)

#### Master Page

`Home.cshtml`

`@{LayoutPage = "Layout.cshtml";}`

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_448B2810.png)

### HTML Helpers

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_150C9377.png)

## Form

```html
<form request="post">
    <input asp-for="email"></label>
```

```cs
var email2 = Request.Form["email"];
//OR
[BindProperty]
public string email { get; set; }  

public async Task<IActionResult> OnPost()
{
    Foo(email);
    return Redirect("/");
}
```

## Query

```cs
// root/?page=1
if(Request.QueryString.HasValue
    && Request.QueryString.Value.Contains("page="))
    string pageInString = Request.Query["page"];
```