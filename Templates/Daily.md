---
created: <% tp.file.creation_date() %>
modified: 2024-03-29T21:35:23+01:00
location: <%* tR += await Promise.race([
    new Promise((resolve) => {
        fetch('http://ip-api.com/json/')
            .then(response => response.json())
            .then(data => 
		        resolve(
			        data.city === 'Järfälla Municipality' ? '"[[Stockholm]]"' : `"[[data.city]]"`
			    )
			)
    }),
    new Promise((resolve) =>
        // If we haven't fetched the location within 300ms,
        // time-out and resolve with the placeholder text instead
        setTimeout(() => resolve('Location'), 300)
    )
])
%>
---
tags: [[Journal]] <% await tp.file.move("/Journal/" + tp.date.now("YYYY-MM-DD")) %>

<< [[Journal/<% tp.date.now("YYYY-MM-DD", -1) %>|Yesterday]] | [[Journal/<% tp.date.now("YYYY-MM-DD", 1) %>|Tomorrow]] >>

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