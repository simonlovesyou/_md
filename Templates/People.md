---
tags:
 - people
phone:
location:
address:
met:
lastname: 
phone:
birthday:
---
<%*
let title = tp.file.title
if (title.startsWith("Untitled")) {
title = await tp.system.prompt("Title");
}
await tp.file.rename(title)
-%>## Notes

- 
