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

Sample document in elasticsearch index.
```json
{
  "_index": "filebeat-7.3.2-2020.05.13-000001",
  "_type": "_doc",
  "_id": "zgrCDnIB_4u5pwHnJkhI",
  "_version": 1,
  "_score": null,
  "_source": {
    "@timestamp": "2020-05-13T15:58:21.681Z",
    "message": "{\"reviewerID\": \"A3EUD541ZM0R0R\", \"asin\": \"B0002E1G5C\", \"reviewerName\": \"Jeff Felker\", \"helpful\": [0, 0], \"reviewText\": \"I own a lot of guitars and have to change strings often enough, I don't really enjoy changing strings but it needs done, this tool makes it such a breeze I don't know how I ever went without it. It takes me a fraction of the time it used to take changing strings, I can have them all loosened and cut in seconds where before I would stand there cranking one tuning peg for what seemed like forever. I am really happy with this purchase and will check out more stuff from Planet Waves.\", \"overall\": 5.0, \"summary\": \"Saves me tons of time and works perfectly\", \"unixReviewTime\": 1396915200, \"reviewTime\": \"04 8, 2014\"}",
    "input": {
      "type": "log"
    },
    "agent": {
      "type": "filebeat",
      "ephemeral_id": "dd93863c-4433-451c-9234-4513b7b25e71",
      "hostname": "618795ab50c5",
      "id": "c9a2f7f2-65b5-417c-b07b-188a0176f163",
      "version": "7.3.2"
    },
    "ecs": {
      "version": "1.0.1"
    },
    "host": {
      "name": "618795ab50c5"
    },
    "log": {
      "offset": 850866,
      "file": {
        "path": "/var/log/sample/app.log"
      }
    }
  },
  "fields": {
    "@timestamp": [
      "2020-05-13T15:58:21.681Z"
    ]
  },
  "sort": [
    1589385501681
  ]
}
```

## References 
- https://logz.io/blog/a-practical-guide-to-kubernetes-logging/
- https://mostafa-asg.github.io/post/ship-app-logs-to-elasticsearch-elk-filebeat/
- https://github.com/cosminseceleanu/tutorials/blob/master/docker-logs-elk/docs/index.md