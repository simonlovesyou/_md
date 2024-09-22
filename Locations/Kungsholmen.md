---
modified: 2024-09-18T20:17:14+02:00
---
## Restaurants
```dataview
TABLE WITHOUT ID file.link as Name, summary as Summary
FROM "Restaurants" and -#MOC
WHERE contains(location, "Kungsholmen")
SORT file.cday DESC
```