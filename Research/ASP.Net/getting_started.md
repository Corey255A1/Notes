# ASP.Net Getting Started
There are plenty of getting started tutorials and a lot of which get out of date in a couple months.

## Requirements
- Visual Studio or Visual Studio Code with C# extensions
- If developing cross platform with Visual Studio code, you'll need the cross platform **dotnet** application.

## Create Project
With full Visual Studio, you can choose the ASP.Net Core Web App as a solution option

With Visual Studio Code
```bash
dotnet new webapp -n StoofApp
```

You'll be started with a basical template website.

## Understand the Project Structure
Once you've created your project, you'll see a structure similar to this:
```
StoofApp/
├── Pages/
│   ├── _ViewImports.cshtml
│   ├── _ViewStart.cshtml
│   ├── Shared/
│   │   └── _Layout.cshtml
│   ├── Index.cshtml
│   ├── Index.cshtml.cs
│   ├── Privacy.cshtml
│   ├── Privacy.cshtml.cs
│   └── Error.cshtml
├── wwwroot/
│   ├── css/
│   ├── js/
│   └── lib/
├── appsettings.json
├── appsettings.Development.json
├── Program.cs
└── StoofApp.csproj
```

**Key directories and files:**

- Pages/: This is where your Razor Pages live.
    - Each Razor Page typically consists of two files:
        - A .cshtml file (e.g., Index.cshtml): This is the view component, containing HTML and Razor syntax (C# code embedded in HTML).
        - A .cshtml.cs file (e.g., Index.cshtml.cs): This is the "code-behind" file, which defines a PageModel class. This class handles HTTP requests (OnGet, OnPost), retrieves data, and prepares it for the .cshtml view.
    - _ViewStart.cshtml: Sets the default layout page for all Razor Pages.
    - _ViewImports.cshtml: Imports namespaces and Tag Helpers that are commonly used across your pages.
    - Shared/_Layout.cshtml: Defines the common HTML structure (header, navigation, footer) for your entire application.
- wwwroot/: Contains static files like CSS, JavaScript, and images. These files are served directly to the browser.
- appsettings.json: Configuration file for your application (e.g., database connection strings, API keys).
- Program.cs: The entry point of your application. It sets up the web host, configures services (like AddRazorPages()), and defines the request processing pipeline.