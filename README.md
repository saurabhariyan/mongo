# MongoDB

- Generic connection string is of the form of : `mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]`

- Delete all the items in a collection : especially while testing it : Prefer `db.your_collection.remove({})` over `db.your_collection.drop()`. This ensures if the collection is capped or if one of the field is marked unique then that is retained in the new collection. 

- [To update a document with an embedded array](https://stackoverflow.com/a/36834252/2517416)

- mongorestore and mongodump are binary restore and dump tools. The output is in bson and hence not human readable. It will be faster than other couterparts in most cases. 

- mongoimport and mongoexport are data import and export where the final data is human readable. It will be slower than the binary counterpart. 
> mongoexport -d db -c collections -q '{ store: { $eq: "xyz" } }' --out /home/xyz.csv

> mongoexport -d test -c records -q '{ a: { $gte: 3 } }' --out exportdir/myRecords.json

> 

- To apply an aggregate over an `$unwind` operator : 

``` db.orders.aggregate([{ $unwind : "$details" }, {$project:{_id:0, "customer":0, "status":1, "notes":0, "ordernum":0, "amount":0, "details.category":1, "details.ean":1, "details.frames":1, "date" : 1, "user":0, "approve_email":0,"lastModified":0, "invoice":1}}])```

```db.orders.aggregate([{ $unwind : "$details" }, {$match:{"status":"shipped"}} , {$project:{_id:0, "amount":0, "details.category":1, "details.name":1, "details.frames":1, "date" : 1, "invoice": 1}}, {$out:'saurabh'}])```

  
