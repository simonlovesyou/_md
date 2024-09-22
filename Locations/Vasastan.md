---
modified: 2024-09-18T21:32:09+02:00
---
## Restaurants
```dataview
TABLE WITHOUT ID file.link as Name, summary as Summary
FROM "Restaurants" and -#MOC
WHERE contains(location, tp.file.name)
SORT file.cday DESC
```