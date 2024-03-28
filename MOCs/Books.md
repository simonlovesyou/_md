[[+Home]] %% tags:: #MOC %% 

```meta-bind-button
label: New Book
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Book.md
    folderPath: Books
    fileName: TKTK
    openNote: true

```

# Book MOC

**Template:** [[Book]]

My Book Maps of Content (MOC) serves as the personalized atlas of my reading journey and related notes.

## Books

### Reading list

```dataview
TABLE summary as Summary, visited as Visited
FROM "Books" and -#MOC
SORT file.cday DESC
```

### Favourites