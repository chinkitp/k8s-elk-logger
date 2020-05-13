# Filebeat to Elasticsearch sink

## How to run the sample?

### Create the elasticsearch stack
```bash
$   docker-compose up 
```

> Wait a 1-2 mins for the stack to start. 

### Write a few lines to the log file. Filebeast will harvest those and insert it into elasticsearch index.
```bash
$   while IFS= read -r line; do echo $line; done < input.log > ./logs/app.log

$ curl -X GET "localhost:9200/filebeat*/_count?pretty"

## output
{
  "count" : 1300,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  }
}
```

### Use Kibana to visualise the data

http://localhost:5601/app/kibana#/management/elasticsearch/index_management/

