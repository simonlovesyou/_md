[[+Home]] #MOC

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
table title
from "Recipes"
sort file.name asc
```