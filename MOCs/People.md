---
prefer-view: read
tags:
  - moc
modified: 2024-04-01T22:10:58+02:00
---
```meta-bind-button
label: New Person
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/People.md
    folderPath: People
    fileName: Name
    openNote: true

```

# People MOC
A personal CRM. People Notes are about jotting down notable information about people.

---
### Templates
- [[Templates/People|People]]

# People
```dataview
table
from "People"
sort file.name asc
```