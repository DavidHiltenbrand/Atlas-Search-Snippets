# Code Sandbox Snippets for Autocomplete
## Query
```json
[
  {
    $search: {
      index: "default",
      "autocomplete": {
        "query": "ca",
//run with "C", then "Ca", then "Car" then "Carl", examining the results with each additional character typed
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
        "analyzer": "lucene.standard"
      }
    }
  }
}
```
## Data Source
```json
[
  {
    "_id": 1,
    "searchField": "Carl Jones"
  },
  {
    "_id": 2,
    "searchField": "Carl Smith"
  },
  {
    "_id": 3,
    "searchField": "Captain Hollingsworth"
  },
  {
    "_id": 4,
    "searchField": "Carey Dearborn"
  },
  {
    "_id": 5,
    "searchField": "Cindy Mills"
  }
]
```
## Results
```json
[
  {
    "_id": 1,
    "searchField": "Carl Jones"
  },
  {
    "_id": 2,
    "searchField": "Carl Smith"
  },
  {
    "_id": 4,
    "searchField": "Carey Dearborn"
  }
]
```
