---
prefer-view: read
tags:
  - moc
modified: 2024-09-22T16:17:24+02:00
---
```meta-bind-button
label: New Recipe
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Recipe.md
    folderPath: Recipes
    fileName: Untitled
    openNote: true

```

# Recipe MOC
A personal CRM. People Notes are about jotting down notable information about people and linking people back to [[Recipes]]

---
### Templates
- [[Recipe]]

# Recipes
```dataview
TABLE WITHOUT ID file.link as Name, duration as Duration
from "Recipes"
sort file.name asc
```