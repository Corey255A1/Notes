# Workflow
## I want to add an item
``` mermaid
flowchart
main[Main Screen]-->add(Select Add Item)-->addscreen[Add Item Screen]
-->useradd([Required Name. Optional photo, location])-->save(Save Item)
```
## I want to view item details
``` mermaid
flowchart
main[Main Screen]-->view(Select View Items)-->viewscreen[Items List Screen]
-->userview([Search, Filter options])-->select(Select Item)-->viewitemscreen[Item Details Screen]
```
## I want to remove an item
``` mermaid
flowchart
start[Item Details Screen]-->remove(Remove Item)-->areyousure
areyousure@{ shape: diamond, label: "Are You Sure?" }
areyousure-- No -->start
areyousure-- Yes -->mainscreen[Items List Screen]
```