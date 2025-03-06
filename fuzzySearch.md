# Code Sandbox Snippets for Fuzzy Search
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
    "name": "William John Doe",
    "description": "This document exactly matches 'John' as our search term, so it receives the highest score."
  },
  {
    "_id": 2,
    "name": "William Joan Doe",
    "description": "This document needs 1 edit to match 'John' as our search term, so it receives the second highest score."
  },
  {
    "_id": 3,
    "name": "William Jan Doe",
    "description": "This document needs 2 edits to match 'John' as our search term, so it receives the third highest score."
  },
  {
    "_id": 4,
    "name": "Bill Smith",
    "description": "This document doesn't match 'John' as our search term even after the maximum 2 edits, so it receives the lowest relevancy score."
  }
]
```
## Results
```json
{
  "documents": [
    {
      "_id": 12,
      "name": "John",
      "description": "This document exactly matches 'John' as our search term, so it receives the highest score.",
      "score": 0.5651124715805054
    },
    {
      "_id": 1,
      "name": "William John Doe",
      "description": "This document exactly matches 'John' as our search term, so it receives the highest score.",
      "score": 0.40346258878707886
    },
    {
      "_id": 2,
      "name": "William Joan Doe",
      "description": "This document needs 1 edit to match 'John' as our search term, so it receives the second highest score.",
      "score": 0.30943524837493896
    },
    {
      "_id": 3,
      "name": "William Jan Doe",
      "description": "This document needs 2 edits to match 'John' as our search term, so it receives the third highest score.",
      "score": 0.15901105105876923
    },
    {
      "_id": 4,
      "name": "Bill Smith",
      "description": "This document doesn't match 'John' as our search term even after the maximum 2 edits, so it receives the lowest relevancy score.",
      "score": 0.03625473752617836
    }
  ]
}
```
