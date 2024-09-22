---
prefer-view: read
tags:
  - moc
modified: 2024-09-18T20:17:49+02:00
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
TABLE WITHOUT ID file.link as Name, location as Location, summary as Summary 
FROM "Restaurants" and -#MOC
SORT file.cday DESC
```