---
prefer-view: read
tags:
  - moc
modified: 2024-06-15T19:51:48+02:00
---
```meta-bind-button
label: New Place
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Place.md
    folderPath: Places
    fileName: Untitled
    openNote: true

```

# Places MOC
A personal CRM. Places Notes are about jotting down notable information about people.

---
### Templates
- [[Place]]

# Places
```dataview
table
from "Places"
sort file.name asc
```