---
prefer-view: read
tags:
  - moc
modified: 2024-04-16T11:26:29+02:00
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
    fileName: Name
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