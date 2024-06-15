---
tags:
  - places
  - city
modified: 2024-06-15T19:39:27+02:00
prefer-view: read
---
<%*
let title = tp.file.title
if (title.startsWith("Untitled")) {
title = await tp.system.prompt("Title");
}
await tp.file.rename(title)
-%>
## 📝 Notes
- 

## Highlights
-

## Restaurants

```dataview  
TABLE WITHOUT ID file.link AS Restaurant, location as Location, summary as Summary
FROM "Restaurants"
WHERE contains(city, link("<% title %>"))
```

## Places

```dataview  
TABLE WITHOUT ID file.link AS Place, location as Location, summary as Summary FROM "Places" WHERE econtains(city, link("<% title %>"))
```
