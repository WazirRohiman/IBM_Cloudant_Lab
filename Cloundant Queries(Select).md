Select all fields in all documents
```
{
   "selector": {}
}
```

Select all fields in all documents with _id greater than 4
```
{
   "selector": {
      "_id": {
         "$gt": "4"
      }
   }
}
```

Select all fields in all documents with _id less than 4
```
{
   "selector": {
      "_id": {
         "$lt": "4"
      }
   }
}
```

Select the fields _id, square_feet and price in all documents
```
{
   "selector": {},
   "fields": [
      "_id",
      "price",
      "square_feet"
   ]
}
```

Select the fields _id, square_feet and price in documents with _id less than 4
```
{
   "selector": {
   "_id": {
         "$lt": "4"
      }
   },
   "fields": [
      "_id",
      "price",
      "square_feet"
   ]
}
```

Select the fields _id, bedrooms and price in documents with _id greater than 2 and sort by _id ascending
```
{
   "selector": {
      "_id": {
         "$gt": "2"
      }
   },
   "fields": [
      "_id",
      "price",
      "square_feet"
   ],
   "sort": [
      {
         "_id": "asc"
      }
   ]
}
```

Select the fields _id, bedrooms and price in documents with _id greater than 2 and sort by _id descending
```
{
   "selector": {
      "_id": {
         "$gt": "2"
      }
   },
   "fields": [
      "_id",
      "price",
      "square_feet"
   ],
   "sort": [
      {
         "_id": "desc"
      }
   ]
}
```

