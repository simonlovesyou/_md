---
prefer-view: read
tags:
  - moc
modified: 2024-09-15T17:16:59+02:00
---
```meta-bind-button
label: New Person
hidden: false
class: ""
tooltip: ""
id: ""
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/People.md
    folderPath: People
    fileName: Untitled
    openNote: true

```

# People MOC
A personal CRM. People Notes are about jotting down notable information about people.

---
### Templates
- [[Templates/People|People]]

# People
```dataviewjs
// People birthdays using DataviewJS
let pages = dv.pages('"People"')

var start = moment().startOf('day');
var end = moment(start).add(dv.current().duration);
var dateformat = "YYYY-MM-DD"

function nextBirthday(birthday) {
    var bday = moment(birthday.toString());
    var bdayNext = moment(bday).year(start.year());
    if (bdayNext.isBefore(start, 'day')) {
        bdayNext.add(1, "year");
    }
    return bdayNext.toDate();
}

function countdown(birthday){
    if(birthday === undefined)
      return undefined

	var bday = moment(birthday.toString())
	const setTime = new Date(bday);
	const nowTime = new Date();
	const restSec = setTime.getTime() - nowTime.getTime();
	const day = parseInt(restSec / (60*60*24*1000));
	return day;
}

console.log({pages: Array.from(pages)})
dv.table(["Name", "Birthday", "Age","Countdown", "Phone"],
  Array.from(pages)
  .sort(p => p.birthday ? moment(p.birthday.toString()).format("MM-DD") : 0, 'asc')
  .sort((personA, personB) => countdown(nextBirthday(personA.birthday)) - countdown(nextBirthday(personB.birthday)))
  .map(p => [
    // The name
    p.file.link,
    // Current age in years
    p.birthday
      ? moment().diff(moment(p.birthday.toString()), 'years') 
      : p.birthday,	
    // Formatted birthday from YAML frontmatter
    p.birthday ? moment(p.birthday.toString()).format("MMMM Do") : p.birthday,
	p.birthday ? `${countdown(nextBirthday(p.birthday))} days` : p.birthday,
	p.phone,
	]
  )
);
```
