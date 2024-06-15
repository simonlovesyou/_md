---
prefer-view: read
tags:
  - moc
modified: 2024-06-15T19:51:57+02:00
---
```meta-bind-button
label: New Restaurant
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Restaurant.md
    folderPath: Restaurants
    fileName: Untitled
    openNote: true

```

# Restaurants MOC

**Template:** [[Restaurant]]

## Restaurants

```dataview
TABLE summary as Summary
FROM "Restaurants" and -#MOC
SORT file.cday DESC
```