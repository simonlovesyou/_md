---
tags:
  - places
  - city
modified: 2024-06-15T19:39:27+02:00
coordinates: 59.3251172,18.0710935
prefer-view: read
---
[[Places]] 

## 📝 Notes
- 

## Highlights
-

## Restaurants

```dataview  
TABLE WITHOUT ID file.link AS Restaurant, location as Location, summary as Summary
FROM "Restaurants"
WHERE contains(city, link("Stockholm"))
```

## Places

```dataview  
TABLE WITHOUT ID file.link AS Place, location as Location, summary as Summary FROM "Places" WHERE econtains(city, link("Stockholm"))
```
