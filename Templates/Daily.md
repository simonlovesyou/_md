---
created: <% tp.file.creation_date() %>
modified: 2024-03-29T21:35:23+01:00
---
tags: [[Journal]] <% await tp.file.move("/Journal/" + tp.date.now("YYYY-MM-DD")) %>

<< [[Timestamps/<% tp.date.now("YYYY", -1) %>/<% tp.date.now("MM-MMMM", -1) %>/<% tp.date.now("YYYY-MM-DD-dddd", -1) %>|Yesterday]] | [[Timestamps/<% tp.date.now("YYYY", 1) %>/<% tp.date.now("MM-MMMM", 1) %>/<% tp.date.now("YYYY-MM-DD-dddd", 1) %>|Tomorrow]] >>

---
## 📅 Daily Questions
### 🌜 Igårkväll efter jobbet så gjorde jag...
- 

### 🙌 Något jag är exalterad för just nu är
- 

### 🚀 Det jag vill åstadkomma idag är...
_Se [[Todo]] för inspiration_
- [ ] 

### 👎 Något jag har svårt med idag...
- 

---
# 📝 Notes
- 
---
### Notes created today
```dataview
List FROM "" WHERE file.cday = date("<%tp.date.now("YYYY-MM-DD")%>") SORT file.ctime asc
```
### Notes last touched today
```dataview
List FROM "" WHERE file.mday = date("<%tp.date.now("YYYY-MM-DD")%>") SORT file.mtime asc
```