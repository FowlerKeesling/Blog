---
publish: true
---
Here stand the evergreens, the old growth of my garden. In this list you will find the books that I have finished, the notes that I have written, and the resources that are ready to be used. This is the heart of my garden and the place I suspect will one day be the most rewarding to explore. Currently it is slim, as this project is still green, but come back after some time and there will likely be much more explore.
```dataview
TABLE
	file.tags AS "Tags"
FROM [[Evergreens]]
WHERE file.name != "index"
AND !contains(file.path, "01 Templates/")
SORT file.name ASC
```

