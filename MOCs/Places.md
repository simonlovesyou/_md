---
prefer-view: read
tags:
  - moc
modified: 2024-07-08T08:52:23+02:00
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

A personal CRM. Places Notes are about jotting down notable information about people.

[[Place|Template]].

## Places
```dataview
table
from "Places"
sort file.name asc
```