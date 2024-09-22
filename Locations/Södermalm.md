---
modified: 2024-09-18T20:16:37+02:00
---
## Restaurants
```dataview
TABLE WITHOUT ID file.link as Name, summary as Summary
FROM "Restaurants" and -#MOC
WHERE contains(location, "Södermalm")
SORT file.cday DESC
```