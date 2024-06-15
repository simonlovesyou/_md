---
tags:
  - city
modified: 2024-06-15T19:58:29+02:00
prefer-view: read
---
## 📝 Notes
- 

## Highlights
-

## Restaurants

```dataview  
TABLE WITHOUT ID file.link AS Restaurant, location as Location, summary as Summary
FROM "Restaurants"
WHERE contains(city, link("Umeå"))
```

## Places

```dataview  
TABLE WITHOUT ID file.link AS Place, location as Location, summary as Summary FROM "Places" WHERE econtains(city, link("Umeå"))
```
