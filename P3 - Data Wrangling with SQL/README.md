# Project 3: OpenStreetMap Data Wrangling with SQL

**Name:** William Autry

**Map Area**

* Location: Atlanta, Georgia
* [OpenStreetMap URL](https://www.openstreetmap.org/relation/119557)
* [MapZen URL](https://s3.amazonaws.com/metro-extracts.mapzen.com/atlanta_georgia.osm.bz2)

I chose the map area of Atlanta, GA where I currently reside. I am interested to find out what insights the queries will reveal.

# 1. Data Audit
###Unique Tags
The XML file contains different types of tags. So, I parsed the Atlanta, GA dataset using ElementTree and counted the number of unique tags.
`mapparser.py` was used to count the number of unique tags.

* ` 'member': 483`
* ` 'nd': 132037,`
* `'node': 117370,`
* `'osm': 1,`
* `'relation': 42,`
* `'tag': 62150,`
* `'way': 8466`

### Patterns in the Tags
The `"k"` value of each tag contains a unique pattern. `tags.py` creates 3 regular expressions to check for certain patterns in the tags.
In total, there are four tag categories:

*  `"lower" : 28859`, for tags that contain only lowercase letters and are valid,
*  `"lower_colon" : 24230`, for otherwise valid tags with a colon in their names,
*  `"problemchars" : 0`, for tags with problematic characters, and
*  `"other" : 9061`, for other tags that do not fall into the previous three categories.

# 2. Problems Encountered in the Map
###Street address inconsistencies
The main problem encountered involved street name inconsistencies. To clean up the dataset, `audit.py` is used to update the original name to a corrected more proper name.
 

* **Abbreviations** 
    * `Ln -> Lane`
* **LowerCase**
    * `suwanee -> Suwanee`
* **Misspelling**
    * `trce -> Trace`


### City name inconsistencies
Using `audit.py`, we update the names

* **LowerCase**
	* `atlanta -> Atlanta`
* **Misspelling**
	* `Atalanta -> Atlanta`


#3. Data Overview
### File sizes:

* `atlanta_georgia.osm: 24.59 GB`
* `atlanta_sample.osm: 24.87 MB`
* `nodes_csv: 9.52 MB`
* `nodes_tags.csv: 745 KB`
* `ways_csv: 548 KB`
* `ways_nodes.csv: 3.02 MB`
* `ways_tags.csv: 1.54 MB`
* `atlanta.db: 17.6 MB`

###Number of nodes:
``` python
sqlite> SELECT COUNT(*) FROM nodes
```
**Output:**
```
117370
```

### Number of ways:
```python
sqlite> SELECT COUNT(*) FROM ways
```
**Output:**
```
8466
```

###Number of unique users:
```python
sqlite> SELECT COUNT(DISTINCT(e.uid))          
FROM (SELECT uid FROM nodes UNION ALL SELECT uid FROM ways) e;
```
**Output:**
```
771
```

###Top contributing users:
```python
sqlite> SELECT e.user, COUNT(*) as num
FROM (SELECT user FROM nodes UNION ALL SELECT user FROM ways) e
GROUP BY e.user
ORDER BY num DESC
LIMIT 10;
```
**Output:**

```
Liber								53040
Saikrishna_FultonCountyImport		24067
woodpeck_fixbot						14693
Jack the Ripper						3544
afonit								3377
rjhale1971							2812
Jack Kittle Buildings				2487
maven149							2064
Chris Lawrence						1257
macon_cfa							1000
```

###Number of users contributing only once:
```python
sqlite> SELECT COUNT(*) 
FROM
    (SELECT e.user, COUNT(*) as num
     FROM (SELECT user FROM nodes UNION ALL SELECT user FROM ways) e
     GROUP BY e.user
     HAVING num=1) u;
```
**Output:**
```
313
```

# 4. Additional Data Exploration

###Common ammenities:
```python
sqlite> SELECT value, COUNT(*) as num
FROM nodes_tags
WHERE key='amenity'
GROUP BY value
ORDER BY num DESC
LIMIT 10;

```
**Output:**
```
place_of_worship	42
```

###Biggest religion:
```python
sqlite> SELECT nodes_tags.value, COUNT(*) as num
FROM nodes_tags 
    JOIN (SELECT DISTINCT(id) FROM nodes_tags WHERE value='place_of_worship') i
    ON nodes_tags.id=i.id
WHERE nodes_tags.key='religion'
GROUP BY nodes_tags.value
ORDER BY num DESC
LIMIT 1;
```
**Output:**
```
Christian :	41
```
###Popular cuisines
```python
sqlite> SELECT nodes_tags.value, COUNT(*) as num
FROM nodes_tags 
    JOIN (SELECT DISTINCT(id) FROM nodes_tags WHERE value='restaurant') i
    ON nodes_tags.id=i.id
WHERE nodes_tags.key='cuisine'
GROUP BY nodes_tags.value
ORDER BY num DESC;
```
**Output:**
```
bar&grill								1
```

# 5. Conclusion
Wrangling the Atlanta, GA dataset showed the data to be of reasonable quality. I did, however, observe some typographical errors caused by human input. By auditing the data I was able to clean up a good amount of observed issues within the data. This project was successful in introducing me to concepts of data wrangling, but the data still could use more improvement. The dataset not only is missing a lot of information, but also contains outdated information. These inadequacies keep the OpenStreetMap from being as reliable as more commercial options.


### Additional Suggestion and Ideas

#### Control typographical errors
* Tie the database back to public postal records to verify certain aspects of each input.
* Develop a script to routinely clean up the data.

#### More information
* The city could use residential tax data and permits to update information that may change.
* Partner with sponsors to offer incentive based data capturing.

# Files
* `Quiz/` : scripts completed in lesson Case Study OpenStreetMap
* `README.md` : this file
* `atlanta_sample.osm`: sample data of the OSM file
* `audit.py` : audit street, city and update their names
* `data.py` : build CSV files from OSM and also parse, clean and shape data
* `database.py` : create database of the CSV files
* `mapparser.py` : find unique tags in the data
* `query.py` : different queries about the database using SQL
* `report.pdf` : pdf of this document
* `sample.py` : extract sample data from the OSM file
* `tags.py` : count multiple patterns in the tags
