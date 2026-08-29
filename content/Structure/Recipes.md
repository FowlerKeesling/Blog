---
publish: true
---
# Welcome Culinary Artist
Here you will find all of the recipes that I tend to make on a regular basis. These recipes are not my own. In the majority of these recipes, you will find a link to the original website. However, song of these recipes were captured long before I started working on this public Thought Garden and I have been unable to track down their source.

---
```dataview
TABLE
FROM [[Recipes]]
WHERE file.name != "index"
AND !contains(file.path, "01 Templates/")
SORT file.name ASC
```
