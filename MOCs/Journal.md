---
prefer-view: read
modified: 2024-04-21T18:40:42+02:00
tags:
  - moc
---
```meta-bind-button
label: New Journal Entry
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Daily.md
    folderPath: Journal
    fileName: TKTK
    openNote: true

```

# Journal MOC
The Journal MOC facilitates easy navigation and connection of diverse journal entries, themes, and reflections. It aids in the development of deeper insights by mapping how different entries relate to each other and to broader life themes.

**Template:** [[Daily]]

## Journal entries

```dataview
TABLE summary
FROM "Journal" and -#MOC
SORT file.name DESC
```