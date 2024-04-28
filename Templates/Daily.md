---
created: <% tp.file.creation_date() %>
modified: 2024-03-29T21:35:23+01:00
tags:
 - journal
location: <%* tR += await Promise.race([
    new Promise((resolve) => {
        fetch('http://ip-api.com/json/')
            .then(response => response.json())
            .then(data => 
		        resolve(
			        data.city === 'Järfälla Municipality' ? '"[[Stockholm]]"' : `"[[${data.city}]]"`
			    )
			)
    }),
    new Promise((resolve) =>
        // If we haven't fetched the location within 300ms,
        // time-out and resolve with the placeholder text instead
        setTimeout(() => resolve('Location'), 3000)
    )
])
%>
---

<%*
const fileName = tp.file.title
const date = tp.date.now("YYYY-MM-DD")
if(!/\d{4}-\d{2}-\d{2}/.test(date)) {
  await tp.file.rename(date)
}
-%><< [[Journal/<% tp.date.now("YYYY-MM-DD", -1) %>|Yesterday]] | [[Journal/<% tp.date.now("YYYY-MM-DD", 1) %>|Tomorrow]] >>

---
## 📅 Daily Questions
### 🌜 Reflektion om gårdagen
- 

### Hur mår jag idag?

### 🚀  Intentioner för idag
_Vad vill jag åstadkomma? Vad vill jag känna, åstadkomma eller lära mig?_
_Se [[Todo]] för inspiration_

### 🙏 Jag är tacksam för...

### Utvecklingsmål

### Hinder att överkomma

### 🙌 Något jag ser framemot idag
- 

### 👎 Något jag har svårt med idag...
- 

### Kreativt


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