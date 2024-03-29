---
prefer-view: read
tags:
  - moc
modified: 2024-03-29T18:35:46+01:00
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
    fileName: RecipeName
    openNote: true

```

# Recipe MOC
A personal CRM. People Notes are about jotting down notable information about people and linking people back to [[🗣 Meetings MOC]].

---
### Templates
- [[Templates/People|People]]

# Recipes
```dataview
table
from "Recipes"
sort file.name asc
```