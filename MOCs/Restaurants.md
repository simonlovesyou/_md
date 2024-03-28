[[+Home]] %% tags:: #MOC %% 

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
TABLE summary as Summary, visited as Visited
FROM "Restaurants" and -#MOC
SORT file.cday DESC
```