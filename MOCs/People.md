[[+Home]] #MOC

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
A personal CRM. People Notes are about jotting down notable information about people and linking people back to [[🗣 Meetings MOC]].

---
### Templates
- [[Templates/People|People]]

# People
```dataview
table title
from "People"
sort file.name asc
```