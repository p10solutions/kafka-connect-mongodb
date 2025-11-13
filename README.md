# kafka-connect-mongodb


```

curl --location 'http://localhost:8083/connectors' \
--header 'Content-Type: application/json' \
--data '{
    "name": "mongo-sink-dynamic-collection-obj-only",
    "config": {
      "connector.class": "com.mongodb.kafka.connect.MongoSinkConnector",
      "tasks.max": "1",
      "topics": "antifraude-events",

      "connection.uri": "mongodb://mongo:27017/?replicaSet=rs0",
      "database": "sales",
      "collection": "fallbackCollection",

      "namespace.mapper": "com.mongodb.kafka.connect.sink.namespace.mapping.FieldPathNamespaceMapper",
      "namespace.mapper.key.collection.field": "CollectionName",
      "namespace.mapper.error.if.invalid": "false",

      "transforms": "ToKey,ExtractObj",
      "transforms.ToKey.type": "org.apache.kafka.connect.transforms.ValueToKey",
      "transforms.ToKey.fields": "CollectionName",
      "transforms.ExtractObj.type": "org.apache.kafka.connect.transforms.ExtractField$Value",
      "transforms.ExtractObj.field": "Object",

      "key.converter": "org.apache.kafka.connect.json.JsonConverter",
      "key.converter.schemas.enable": "false",
      "value.converter": "org.apache.kafka.connect.json.JsonConverter",
      "value.converter.schemas.enable": "false",

      "document.id.strategy": "com.mongodb.kafka.connect.sink.processor.id.strategy.BsonOidStrategy",
      "writemodel.strategy": "com.mongodb.kafka.connect.sink.writemodel.strategy.InsertOneDefaultStrategy",

      "errors.tolerance": "all"
    }
  }'

```
