---
prefer-view: read
tags:
  - moc
modified: 2024-06-15T19:51:53+02:00
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
table
from "Recipes"
sort file.name asc
```