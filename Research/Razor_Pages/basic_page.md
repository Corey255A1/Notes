# Create a basic Razor Page
Let's create a simple "About" page to see how it works.

In the Pages folder, right-click and choose "Add" > "Razor Page..." (in Visual Studio) or manually create two files: About.cshtml and About.cshtml.cs.

## Pages/About.cshtml:

```HTML
@page
@model StoofApp.Pages.AboutModel
@{
    ViewData["Title"] = "About Us";
}

<h1>@ViewData["Title"]</h1>

<p>This is the About page for Stoof.</p>
<p>@Model.Message</p>
```

- @page: This directive makes the file a Razor Page, enabling it to handle requests directly.
- @model StoofApp.Pages.AboutModel: Binds this page to its PageModel class.
- @{ ViewData["Title"] = "About Us"; }: Sets the title for the page, which is then used in _Layout.cshtml.
- @Model.Message: This demonstrates how to access properties from your PageModel.

## Pages/About.cshtml.cs:
```c#
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;

namespace StoofApp.Pages
{
    public class AboutModel : PageModel
    {
        public string Message { get; set; } = "Welcome to our app!";

        public void OnGet()
        {
            // This method is called when the page is requested via GET.
            // You can perform data retrieval or setup here.
            Message = "Learn more about what we do.";
        }

        public void OnPost()
        {
            // This method is called when a form is submitted to this page via POST.
            // You'd handle form data here.
        }
    }
}
```

- public class AboutModel : PageModel: Your page's logic class inherits from PageModel.
- public string Message { get; set; }: A property that can be accessed by your .cshtml view.
- OnGet(): The handler method for HTTP GET requests.
- OnPost(): The handler method for HTTP POST requests (useful for forms).

## Add a Link to Your New Page

To make your "About" page accessible, add a link to it in your Pages/Shared/_Layout.cshtml file:

Find the ``<ul class="navbar-nav flex-grow-1">`` section and add a new list item:

```html
<li class="nav-item">
    <a class="nav-link text-dark" asp-area="" asp-page="/About">About</a>
</li>
```

- asp-page="/About": This is a Tag Helper that generates the correct URL for your Razor Page. The /About refers to Pages/About.cshtml.