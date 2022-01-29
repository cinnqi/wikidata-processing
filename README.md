# NIL-entities File creation

## Data Source Used
[wikidata-20170213-all.json: 9.9G](https://archive.org/download/wikibase-wikidatawiki-20170213/wikidata-20170213-all.json.gz)

[wikidata-20210419-all.json.gz: 91.8G](https://archive.org/download/wikibase-wikidatawiki-20210419/wikidata-20210419-all.json.gz)

## Objective of Creation
Listing entities that are stored in wikidata2021 but do not exist in wikidata2017 according to a defined output format.
## Defined Output Format
The final result should include entity id, name, description, wikisitelink, as well as mainsnaks.
## Output File Details 
* **file location:** /home/chengxi/data_process/entities_json_data
* **file size:** 
* **format:** json zipped file(.gz)
## Output File Content 
### Top Level Structure
```
  {
  "id": "Q801899",
  "english_label": "Madrid\u2013Barcelona railway",
  "english_desc": "railway line",
  "wiki_sitelink": "Madrid\u2013Barcelona railway",
  "mainsnaks": []
}
```
The final output file contains one entity per line. In each entity, the attributes list above. Among them, mainsnaks are extracted from the claim of the original data, and its specific content is as follows.
```
  [
      {
        "snaktype":"value",
        "property":"P1064",
        "datavalue":{
          "value":{
            "entity-type":"item",
            "numeric-id":3319112,
            "id":"Q3319112"
          },
          "type":"wikibase-entityid"
        },
        "datatype":"wikibase-item"
      },
      {
        "snaktype":"value",
        "property":"P31",
        "datavalue":{
          "value":{
            "entity-type":"item",
            "numeric-id":728937,
            "id":"Q728937"
          },
          "type":"wikibase-entityid"
        },
        "datatype":"wikibase-item"
      },
      ........
    ]
```

## Creation Steps
1. Extract desired fields using pydash. Especially deal with 'minsnaks' which are nested in 'claims'.
2. Creat a list to store id in wikidata2017.
3. Traverse the entities in 2021, compare the IDs with 2017, if they are the same, delete the corresponding IDs from the list(a match, deleting for reducing running time), and this entity will not be written to the file as a new entity.
4. After one iteration for wikidata2021, output the final files.


