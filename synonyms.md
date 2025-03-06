# Code Sandbox Snippets for Synonyms
## Query
```json
[
  {
    $search: {
      index: "default",
      text: {
        query: "John",
        path: {
          wildcard: "*"
        },
        fuzzy: {maxEdits: 2 }
      },
      scoreDetails: true
    }
  },
  {
    "$project": {
      "_id": 1,
      "name": 1,
      "description": 1,
      "score": { "$meta": "searchScore" },
      //"scoreDetails": { "$meta": "searchScoreDetails" }
    }
  }
]
```
## Index
```json
{
  "mappings": {
    "dynamic": true
  }
}
```
## Data Source
```json
[
  {
    "_id": 1,
    "field": "value"
  },
  {
    "_id": 2,
    "field": "value"
  },
  {
    "_id": 3,
    "field": "value"
  },
  {
    "_id": 4,
    "field": "value"
  }
]
```
## Results
```json
{
  "documents": [
    {
    },
    {
    }
  ]
}
```
