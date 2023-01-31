## Connecting to Cloundant instance using curl and api url
Get your cloundant url from the service credential of the your cloundant instance
The url below is a dummy url for example only
```
"https://apikey-v2-1ktn8d6fuuo6kjoz145fris5ccx24fhmirsku7o3q7bh:6b3dc2399426437b2397e08ac9cf0184@4646e655-6aee-42d8-8b93-d2bde6e9a6ca-bluemix.cloudantnosqldb.appdomain.cloud"
```

On the terminal, save the url into a variable called CLOUDANTURL
```
export CLOUDANTURL="https://apikey-v2-1ktn8d6fuuo6kjoz145fris5ccx24fhmirsku7o3q7bh:6b3dc2399426437b2397e08ac9cf0184@4646e655-6aee-42d8-8b93-d2bde6e9a6ca-bluemix.cloudantnosqldb.appdomain.cloud"
```

Use curl to test your connection to your Cloundant server
```
curl $CLOUDANTURL
```

To test if your credentials, you can attempt to get a list of all your databases in the server
```
curl $CLOUDANTURL/_all_dbs
```

To create a new database(in this case called animals) on your Cloundant server, run the curl PUT command, don't forget the ```-X```
```
curl -X PUT $CLOUDANTURL/animals
```

To drop the animals database, use the following curl command
```
curl -X DELETE $CLOUDANTURL/animals
```

Create a new database called 'planets'
```
curl -X PUT $CLOUDANTURL/planets
```

---------------------------------------------------------------------------------------------------------
## Inserting and updating Cloudant database documents

To insert a document in the planets database with _id of “1”, use the following curl command
We use put instead of post because we are assigning an "_id" of 1 manually. Using 'post' will automatically assign an id to the document
```
curl -X PUT $CLOUDANTURL/planets/"1" -d '{
      "name" : "mercury",
      "position_from_sun": 1
      }'
```

You can verify the new listing using the following

Save the '_rev' for later. 
```
"_rev":"1-9cfab99684274963c2e7aed91b67ded2"
```

To update a document, you need it's revision id (like the one above)
```
curl -X PUT $CLOUDANTURL/planets/1 -d '{"name":"Mercury" , "position_from_sum":1, "revolution_time":"88 days", "_rev":"1-9cfab99684274963c2e7aed91b67ded2"}'
```

Verify if the above command was successfull
```
curl -X GET $CLOUDANTURL/planets/1 
```

Once again save the "_rev" value. In this case after the update, the line below is the new rev value
```
"_rev":"2-897f4f525235bc3d1ed23e5eb85f588c"
```

Make another update by adding the 'rotation_time' key-value pair - Don't forget to insert the 1st _rev value into the 2nd update.
```
curl -X PUT $CLOUDANTURL/planets/1 -d '{"name": "Mercury", "position_from_sum": 1, "revolution_time": "88 days", "rotation_time": "59 days", "_rev": "2-897f4f525235bc3d1ed23e5eb85f588c"}'
```

Verify again if the above command was successful and save the revision value
```
curl -X GET $CLOUDANTURL/planets/1
```

```
"_rev":"3-805352af7d60bd2767941d2808239ac2"
```

To delete a document you will need the latest revision ID. Use the command below and insert the _rev id for document 1 in the syntax
```
curl -X DELETE $CLOUDANTURL/planets/1?rev=3-805352af7d60bd2767941d2808239ac2
```

-----------------------------------------------------------------------------------------------------------------------------------
## Querying Cloundant Database with curl

Use Post when querying (from 'diamond' database)

Query for diamond with _id 1
```
curl -X POST $CLOUDANTURL/diamonds/_find \-H"Content-Type: application/json" \-d'{ "selector":{"_id":"1"}}'
```

Query for diamonds with carat size of 0.3
```
curl -X POST $CLOUDANTURL/diamonds/_find \-H"Content-Type: application/json" \-d'{ "selector":{"carat":0.3}}'
```

Query for diamonds with price more than 345
```
curl -X POST $CLOUDANTURL/diamonds/_find \-H"Content-Type: application/json" \-d'{ "selector":{"price":{"$gt":345}}}'
```

--------------------------------------------------------------------------------------------------------------------------
## Creating indexes

Noticed the ‘Warning’: “No matching index found, create an index to optimize query time.” in the output of previous queries. That is Cloudant telling you that, you are running a query on a field that is not indexed.

Create an index on the key “price”
```
curl -X POST $CLOUDANTURL/diamonds/_index \-H"Content-Type: application/json" \-d'{"index": {"fields": ["price"]}}'
```




