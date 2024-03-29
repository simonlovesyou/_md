---
prefer-view: read
tags:
  - moc
modified: 2024-03-29T18:55:24+01:00
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
    fileName: TKTK
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