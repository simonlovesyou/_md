---
prefer-view: read
tags:
  - moc
modified: 2024-06-15T19:48:39+02:00
---
```meta-bind-button
label: New City
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/City.md
    folderPath: Cities
    fileName: Untitled
    openNote: true

```

# City MOC
A personal CRM. Places Notes are about jotting down notable information about cities.

---
### Templates
- [[City]]

# Places
```dataview
table
from "Cities"
sort file.name asc
```