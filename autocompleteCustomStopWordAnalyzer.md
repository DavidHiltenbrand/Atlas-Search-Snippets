# Code Sandbox Snippets for Fuzzy Search
## Query
```json
[
  {
    $search: {
      index: "default",
      "autocomplete": {
        "query": "Dr. Smi",
//run with "Dr. S", then "Dr. Sm", then "Dr. Smi", then finally "Dr. Smithf", examining the results with each additional character typed
        "path": "searchField"
      }
    }
  }
]
```
## Index
```json
{
  "mappings": {
    "dynamic": true,
    "fields": {
      "searchField": {
        "type": "autocomplete",
        "analyzer": "customStopWord"
      }
    }
  },
  "analyzers": [
    {
      "name": "customStopWord",
      "charFilters": [],
      "tokenizer": {
        "type": "whitespace"
      },
      "tokenFilters": [{
          "type": "stopword",
          "tokens": ["Doctor", "Dr."]
        }]
    }
  ]
}
```
## Data Source
```json
[
  {
    "_id": 1,
    "searchField": "Doctor Smithwick"
  },
  {
    "_id": 2,
    "searchField": "Doctor Smithsonian"
  },
  {
    "_id": 3,
    "searchField": "Doctor Williamson"
  },
  {
    "_id": 4,
    "searchField": "Dr. Smithfield"
  },
  {
    "_id": 5,
    "searchField": "Dr. Smead"
  }
]
```
## Results
```json
{
  "documents": [
    {
      "_id": 1,
      "searchField": "Doctor Smithwick"
    },
    {
      "_id": 2,
      "searchField": "Doctor Smithsonian"
    },
    {
      "_id": 4,
      "searchField": "Dr. Smithfield"
    }
  ]
}
```
