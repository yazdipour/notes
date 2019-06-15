# ASP

## Startup

```cs
// Startup()
private readonly IConfigurationRoot configuration;
configuration = new ConfigurationBuilder()
                    .AddEnvironmentVariables()
                    .AddJsonFile(env.ContentRootPath + "/config.json")
                    .AddJsonFile(env.ContentRootPath + "/config.development.json", true)
                    .Build();


// ConfigureServices()
services.AddMvc();
class FeatureToggles{bool EnableDeveloperExceptions = false;}
services.AddTransient<FeatureToggles>(x => new FeatureToggles { EnableDeveloperExceptions = configuration.GetValue<bool>("FeatureToggles:EnableDeveloperExceptions")});
// {"FeatureToggles": {"EnableDeveloperExceptions": true}}
if(configuration["FeatureToggles:EnableDeveloperExceptions"]=="True"){}


// Configure(+1 FeatureToggles)
app.UseExceptionHandler("/error.html"); // 404 for users
if(features.EnableDeveloperExceptions) app.UseDeveloperExceptionPage();
app.Use(async (context, next) =>
{
    if (context.Request.Path.Value.Contains("invalid")) throw new Exception("ERROR!");
    await next(); // Continues Configure()!!
});
app.UseFileServer(); //use wwwroot
```

## Routes

```cs
app.UseMvc(routes =>
    routes.MapRoute("Default","{controller=Home}/{action=Index}/{id?}"));
// {controller = defaultControl}
// {action = Index}
// {id:int?} Optional Integer
```

![filters](assets/asp/routes.jpg)

## DI

* Transient: Shortest lifespan - An insstance will be created everytime one is requested.
* Scoped: A single instance will be created for each "scope". In ASP, the "scope" is almost always the current web request.
* Singleton: A single instance will be created for the entire application.

## MVC

ViewPage is dynamic typed. Its like a Dictionary.

### Controller

```cs
[Route("blog")]
public class BlogController : Controller{
    //GET: /blog/ - When defining Route[""], /blog/index will not work.
    [Route("")]
    public IActionResult Index(){
        var posts = new[]{new Post{},new Post{}};
        return View(posts);
        // return new ContentResult{Content="RawHtml"};
    }
    //GET: /blog/Post/2000/12/key
    [Route("{year:min(2000)}/{month:range(1,12)}/{key}")]
    public IActionResult Post(int year, int? month, string key)
    {
        if(month==null){}
        var post = new Post { Title = "My blog post", ...};
        return View(post);
    }
```

### View

```html
<!-- // Views/Blog/Index.cshtml -->
@model IEnumerable<Models.Post>
@{
    Layout = "_Layout";
}
<h1>Explorer's Blog</h1>
<p>
    Below are a few of the latest posts from some of our explorers.
</p>
<div class="blog-posts">
    @foreach (var post in Model)
        @Html.Partial("_Post", post)
</div>

<!-- // Views/Blog/Post.cshtml -->
@model Models.Post
@{
    Layout = "_Layout";
}
@Html.Partial("_Post") // default gets parent model
@Html.Partial("_Post", model)

<!-- // Views/Shared/_Post.cshtml -->
<!-- PartialView -->
@inject Models.FormattingService Format
@model Models.Post
@section header { <!-- IsSectionDefined Checks this -->
    <h1>Explore our world your way</h1>
    <a href="/tours.htm" title="Find your tour!"><h2>Find your tour</h2></a>
}
<article class="blog-post">
    <h1>@Model.Title</h1>
    <div class="details">
        Posted <span>@Format.AsReadableDate(Model.Posted)</span> by <span>@Model.Author</span>
    </div>
    <div class="content">
        @Model.Body
    </div>
</article>

<!-- // Views/Shared/_Layout.cshtml -->
<!DOCTYPE HTML>
<html lang="en">
    ...
    <a href="@Url.Action("Index", "Blog")" title="read our blog!">Read our Blog</a>
<section id="actionCall">
      @if (IsSectionDefined("header"))
        @RenderSection("header", false)
      else
          <h1>Explore our world your way</h1>
  </section>
  <div id="contentWrapper">
  <section id="mainContent"> @RenderBody() </section>
    <aside id="secondaryContent">
        <div id="specials" class="callOut">
            @await (Component.InvokeAsync<ViewComponents.MonthlySpecialsViewComponent>())
        </div>
    </aside>
  </div>
  <footer id="pageFooter"> Copyright Me @DateTime.Now.Year </footer>
</html>
```

### ViewComponent

```cs
///ViewComponents/XViewComponent.cs
[ViewComponent]
class XViewComponent : ViewComponent
    public IViewComponentResult Invoke() => new View();

// USING IT in Home/index.cshtml
<div>@await (Component.InvokeAsync<ViewComponents.XViewComponent>())</div>
// View of XViewComponent.cshtml needs to be in
// Views/Home/Components/XViewComponent.cshtml
// OR
// Views/Shared/Components/XViewComponent.cshtml
```

### ViewStart

Views/_ViewStart.cshtml addes to every view

```cs
@{
    Layout = "_Layout";
}
```

## Partial Rendering with AJAX

```cs
// Views/Blog/Index.cshtml
@if (ViewBag.HasNextPage) {
    <a class="next" href="@Url.Action("Index", "Blog", new { page = ViewBag.NextPage })"> Next </a>
// Controllers/BlogController
[Route("")]
public IActionResult Index(int page = 0)
    if (Request.Headers["X-Requested-With"] == "XMLHttpRequest")
        return PartialView(posts);
    return View(posts);
```

```js
$(function () {
    $('#mainContent').on('click', '.next a', function () {
        var url = $(this).attr('href');
        $('#mainContent').load(url);
        return false;
    })
})
```

## Injectable Services - Formatter - Converter

```cs
namespace Models
    public class FormattingService
        public string AsReadableDate(DateTime date) => date.ToString("D");

public class Startup
    public void ConfigureServices(IServiceCollection services)
        services.AddTransient<FormattingService>();

// cshtml
@inject Models.FormattingService Format
Posted @Format.AsReadableDate(Model.Posted)
```

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

## Form

### Build Form

#### HTML Helpers

![](https://aspblogs.blob.core.windows.net/media/scottgu/Media/image_thumb_150C9377.png)

```html
<form asp-action="Create" asp-controller="Blog" request="post">>

    <div asp-validation-summary="ModelOnly" class="input-validation-error"></div>
    <!-- ModelOnly, All, None -->
    <p>
        <label asp-for="Title"></label>
        <input asp-for="Title" class="form-control" placeholder="Blog post title" />
        <span asp-validation-for="Title"></span>
    </p>
    <input asp-for="email"></label>
    <!-- asp-for put this attr in model.email -->
```

#### Tag Helpers

```cs
@using (Html.BeginForm())
{
    @Html.ValidationSummary()

    @Html.Label("Name: ")
    @Html.TextBoxFor(m=>m.Id) <br/>
    @Html.EditorFor(x => x.Title)
    @Html.ValidationMessageFor(x => x.Title)
    
    <button type="submit" value="submit">Submit</button>
}
```

### Reciveing

```cs
// In Controller
var email2 = Request.Form["email"];
//OR
[BindProperty]
public string email { get; set; }  

public async Task<IActionResult> OnPost()
{
    Foo(email);
    return Redirect("/");
}
//OR
[HttpPost, Route("/")] //HttpGet for Get part
public async Task<IActionResult> OnPost(ReturningObjType obj)
{
    Foo(email);
    return new View();
}
```

## Query

```cs
// root/?page=1
if(Request.QueryString.HasValue
    && Request.QueryString.Value.Contains("page="))
    string pageInString = Request.Query["page"];
```

## Validate Input Data

```cs
[Required]
[Display(Name = "Post Title")] // for Label in HTML
[DataType(DataType.Text)] // DataType.Password & MultilineText ...
[StringLength(100, MinimumLength = 5, ErrorMessage = "Title must be 5 and 100 char long")]
public string Title { get; set; }

public string Author { get; set; }

[Required]
[MinLength(100, ErrorMessage = "Blog posts must be at least 100 chars long")]
[DataType(DataType.MultilineText)]
public string Body { get; set; }

[Compare("Password", ErrorMessage = "Passwords must match")]
[Display(Name = "Confirm Password")]
public string ConfirmPassword { get; set; }
// Call it in Form to Validate
@using (Html.BeginForm())
        @Html.ValidationSummary()

// Get Result
// In Controller
[HttpPost, Route("/")]
public async Task<IActionResult> OnPost(ReturningObjType obj)
{
     if (!ModelState.IsValid) return View();
```

## Entity Framework

### Setup

```cs
public class BlogDataContext : DbContext
    public DbSet<Post> Posts { get; set; } //TABLE
    public BlogDataContext(DbContextOptions<BlogDataContext> options): base(options)
        => Database.EnsureCreated(); //Connect if DB exists, create if not

// Startup.cs / ConfigureServices
services.AddDbContext<BlogDataContext>(option => option.UseSqlServer(connectionString););
//example.
connectionString = "Server=(localdb)\\mssqllocaldb;Database=ExploreCalifornia;Trusted_Connection=True;"
```

### Using

```cs
//BlogController
private readonly BlogDataContext _db;
public BlogController(BlogDataContext db) => _db = db;
//Using to Write
_db.Posts.Add(post);
_db.SaveChanges();
//Using to Read
var post = _db.Posts.FirstOrDefault(x => x.Key == key);
var posts = _db.Posts.OrderByDescending(x => x.Posted).Take(5).ToArray();
```

## API

/Api/CommentsController.cs

```cs
[Route("api/posts/{postKey}/comments")]
public class CommentsController : Controller
    private readonly BlogDataContext _db;
    public CommentsController(BlogDataContext db) => _db = db;
// GET: api/values
[HttpGet]
public IQueryable<Comment> Get(string postKey) => return _db.Comments.Where(x => x.Post.Key == postKey);
// GET api/values/5
[HttpGet("{id}")]
public Comment Get(long id) => _db.Comments.FirstOrDefault(x => x.Id == id);
// POST api/values
[HttpPost]
public Comment Post(string postKey, [FromBody]Comment comment)
    var post = _db.Posts.FirstOrDefault(x => x.Key == postKey);
    comment.Post = post;
    _db.Comments.Add(comment);
    _db.SaveChanges();
    return comment;
// PUT api/values/5 - To Update Comment
[HttpPut("{id}")]
public IActionResult Put(long id, [FromBody]Comment updated)
// DELETE api/values/5 - To Delete Comment
[HttpDelete("{id}")]
public void Delete(long id)
```

## Identity Services

* Basic Impl  with Login/Reg Page: https://github.com/jchadwick/LearnAspNetCoreMvc/tree/Ch06/06_04_End
* Add `[Authorize]` before Actions to limit access.
* Config

```cs
// Startup.ConfigureServices()
services.AddIdentity<IdentityUser, IdentityRole>()
    .AddEntityFrameworkStores<IdentityDataContext>(); //To store in DB
services.AddMvc();

// Startup.Configure
app.UseIdentity();
app.UseMvc(routes => ...
```

* Models/IdentityDataContext.cs

```cs
public class IdentityDataContext : IdentityDbContext<IdentityUser> /// **IdentityDbContext**
    public IdentityDataContext(DbContextOptions<IdentityDataContext> options) : base(options)
            => Database.EnsureCreated();
```

## CSRF (cross-site request forgery)

Add

```html
<form role="form" asp-action="Login"
    asp-antiforgery="true">
<!-- OR ADD THIS AFTER -->
    @Html.AntiForgeryToken()
```

Check

```cs
// AccountController
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> Login
```
