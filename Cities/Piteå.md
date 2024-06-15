---
tags:
  - places
  - city
modified: 2024-06-15T19:43:09+02:00
coordinates: 65.3134652,21.4900252
---
[[Places]] 

## 📝 Notes
- Piteå kommer från ett samiskt ord som betyder ungefär brant backe eller brink och ska alltså syfta på de branta stränderna som vi kan se vid bl.a Arnemark.
	- Vad Piteå egentligen betyder är inte klarlagt.
- Pitesamiskan är ett av världens mest hotade språk och ett av de minsta i världen. Det är alltså få som talar pitesamiska i dag.
- Piteås födelsedag är ungefär 12 maj 1621.

## Highlights
- 

## Restaurants
```dataview  
TABLE WITHOUT ID file.link AS Restaurant, location as Location, summary as Summary
FROM "Restaurants"
WHERE econtains(city, link("Piteå"))
```
## Places
```dataview  
TABLE WITHOUT ID file.link AS Restaurant, location as Location, summary as Summary
FROM "Places"
WHERE econtains(city, link("Piteå"))
```