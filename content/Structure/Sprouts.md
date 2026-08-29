---
publish: true
---
Here you will find my sprouts, they contain all of the ideas that are currently being cultivated. Some may be close to maturation, others are fresh out of the nursery. This is the home of my learning and the place I am currently spending most of my time.
```dataview
TABLE
	file.tags AS "Tags"
FROM [[Sprouts]]
WHERE file.name != "index"
AND !contains(file.path, "01 Templates/")
SORT file.name ASC
```
