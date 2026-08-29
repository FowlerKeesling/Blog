---
publish: true
---
Here you will find all of my seeds, filled with potential and waiting patiently to be cultivated. It contains the books I want to read, the ideas I want to explore, and the thoughts I have had that are worthy of investigation.
```dataview
TABLE
	file.tags AS "Tags"
FROM [[Seeds]]
WHERE file.name != "index"
AND !contains(file.path, "01 Templates/")
SORT file.name ASC
```

