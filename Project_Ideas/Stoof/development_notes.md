# Dev Notes
## HTTPS Default Random Issue
I started a new Visual Studio 2022 ASP.Net Project project for Razor Pages. I kept the *configure for HTTPS* option selected.. which now Edge won't let me open the default page because it says it sent scrambled credentials. I ended the application (Stopped debugging) and started it back up, and now it seems to be working.

## General
The **wwwroot** includes bootstrap and jquery by default.

## Dependencies
- **Microsoft.EntityFrameworkCore** 
- To use SQLite database **EntityFrameworkCore.Sqlite**
- To run migrations and do other database maintenance stuff from the console **Microsoft.EntityFrameworkCore.Tools**

## Adding a controller router
I wanted to get started with a basic API. 

Create a folder named Controllers.
Add a new C# class in Controllers named ItemsController.cs:
```c#
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class ItemsController : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok(new { message = "Hello from Stoof API!" });
    }
}
```

This gives you an endpoint at /api/items that returns a basic JSON message.

In Startup.cs (ASP.NET Core 5 or earlier) or Program.cs (ASP.NET 6+), make sure to include **controller mapping**.
For ASP.NET Core 6+:
```c#
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddControllers();
builder.Services.AddRazorPages();

var app = builder.Build();

// Add this VV
app.MapControllers();   // Enables route to /api/items
// ^^
app.MapRazorPages();    // Keeps Razor UI working
app.Run();
```

Run this and navigate to **https://localhost:7101/api/items** and you will see the json response!
```json
{"message":"Hello from Stoof API!"}
```

## Connecting a database
In a Models folder, create Item.cs:
```c#
public class Item
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int? LocationId { get; set; }
}
```

In the same Models folder, add StoofContext.cs:
```c#
using Microsoft.EntityFrameworkCore;

public class StoofContext : DbContext
{
    public StoofContext(DbContextOptions<StoofContext> options)
        : base(options)
    {
    }

    public DbSet<Item> Items { get; set; }
}
```

Open Program.cs and add the SQLite provider:
```c#
builder.Services.AddDbContext<StoofContext>(options =>
    options.UseSqlite("Data Source=stoof.db"));
```

(This creates your SQLite file and schema.)  
💡 You’ll need the Microsoft.EntityFrameworkCore.Sqlite and Microsoft.EntityFrameworkCore.Tools packages installed.

Open Package Manager Console and run:
- Add-Migration InitialCreate
- Update-Database

If this commands are not found, ensure the Tools package is installed




Back in ItemsController.cs, inject the context and fetch the items:
```c#
[ApiController]
[Route("api/[controller]")]
public class ItemsController : ControllerBase
{
    private readonly StoofContext _context;

    public ItemsController(StoofContext context)
    {
        _context = context;
    }

    [HttpGet]
    public async Task<IActionResult> Get()
    {
        var items = await _context.Items.ToListAsync();
        return Ok(items);
    }
}
```

If there were things in the database the endpoint will now return JSON like:
```json
[
  { "id": 1, "name": "Travel Charger", "locationId": 2 },
  { "id": 2, "name": "Spare Socks", "locationId": 4 }
]
```





