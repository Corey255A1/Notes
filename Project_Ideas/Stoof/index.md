# Stoof
There are lots of apps out in the world that track inventory. The idea that makes this different is that I want specifically a way to track where things are during travel or other temporary locations. We were planning on traveling with a lot of stuff in pouches and pockets of our suitcases and backpacks. I thought it would be interesting to have an app that could tell you which pocket or subcompartment something is in.

I want this to be self hostable so that I can run it as a container on my NAS.

I also wanted to take this oppotunity to work on my software architecture and planning skills.

## User Stories
### As a user I want to
- Manage Items
    - Add, Remove, Update inventory items
    - View a list of all items
    - Filter, sort, search the items
    - Take photographs or upload pictures of items
    - Specify the location of items
    - Specify temporary locations
        - They can be made permanent or reverted once returned to original location
    - Define custom item categories
- Manage Locations
    - Add, Remove, Update inventory locations
    - View a list of all locations
    - Filter, sort, search the locations
    - View list of items by location
    - Take photographs or upload pictures of locations
        - Group photographs of same location to show sublocations
    - Define locations as a tree (parent/child)
    - Specify hotspots on images to show locations of sublocations
    - Define custom location categories

### Workflow
#### I want to add an item
``` mermaid
flowchart
main[Main Screen]-->add(Select Add Item)-->addscreen[Add Item Screen]
-->useradd([Required Name. Optional photo, location])-->save(Save Item)
```
#### I want to view item details
``` mermaid
flowchart
main[Main Screen]-->view(Select View Items)-->viewscreen[Items List Screen]
-->userview([Search, Filter options])-->select(Select Item)-->viewitemscreen[Item Details Screen]
```
#### I want to remove an item
``` mermaid
flowchart
Start[Item Details Screen]-->remove(Remove Item)-->areyousure([Are you sure?])-->goback/remove(Go Back or Delete)
```
### Edge Cases
- Handling items of multiple quantities
    - Things like Chargers, Towels, Clothing, paper towel rolls
    - Also things that are similar but different (different colors or brands, year models)


## Tech Stack
At its most basic, this is just a CRUD app. Naturally this should have a database to manage the items and locations. Since I'm going for simplicity, just going to use SQLite.
When storing pictures, this can just be a file server location that is mounted by the container.
### Tables
- Items
- Locations
- Pictures
- Categories
- PictureHotSpots
- ItemCategories
- ItemPictures
- LocationPictures
- PictureCategories


I'm most comfortable with C# therefore ASP.Net is what I'm going to choose for the backend service.

Front end does not have to be realtime. Sticking with simple Razor pages should be good enough.
