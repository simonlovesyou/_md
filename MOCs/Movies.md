---
prefer-view: read
modified: 2024-03-31T15:31:17+02:00
tags:
  - moc
---
```meta-bind-button
label: New Movie
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Movie.md
    folderPath: Movies
    fileName: TKTK
    openNote: true

```

# Book MOC

**Template:** [[Book]]

My Book Maps of Content (MOC) serves as the personalized atlas of my reading journey and related notes.

## Books

### Reading list

```dataview
TABLE summary as Summary
FROM "Books" and -#MOC
SORT file.cday DESC
```

### Favourites