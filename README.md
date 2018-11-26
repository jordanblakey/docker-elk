# Learning The ELK Stack

## Agenda

Setup Elasticsearch, Logstash and Kibana (ELK) using Docker Containers.

## Terms

*ElasticSearch*: Elasticsearch is an open source distributed, RESTful search and analytics engine capable of solving a growing number of use cases.

*LogStash*: Logstash is an open source, server-side data processing pipeline that ingests data from a multitude of sources simultaneously, transforms it, and sends it to Elasticsearch.

*Kibana* : Elasticsearch is an open source distributed, RESTful search and analytics engine capable of solving a growing number of use cases.

*Apache Lucene*: While suitable for any application that requires full text indexing and searching capability, Lucene has been widely recognized for its utility in the implementation of Internet search engines and local, single-site searching. Lucene includes a feature to perform a fuzzy search based on edit distance.

### Run Elasticsearch + Kibana + Logstash using Docker

```sh
docker-compose build # If you change the ELK_VERSION in /.env
docker-compose up
curl http://localhost:5601 # Check Kibana up and running
curl http://localhost:9200 # Check Elasticsearch up and running

```

### ELK endpoints

```sh
curl -X GET "localhost:9200/_cat" # SHOW ALL COMMANDS
curl -X GET "localhost:9200/_cat/health?v" # ?v is for verbose. Shows Column names
curl -X GET "localhost:9200/_cat/nodes?v"
curl -X GET "localhost:9200/_cat/indices?v"
curl -X GET "localhost:9200/_cat/allocation"
curl -X GET "localhost:9200/_cat/shards"
curl -X GET "localhost:9200/_cat/shards/{index}"
curl -X GET "localhost:9200/_cat/master"
curl -X GET "localhost:9200/_cat/nodes"
curl -X GET "localhost:9200/_cat/tasks"
curl -X GET "localhost:9200/_cat/indices"
curl -X GET "localhost:9200/_cat/indices/{index}"
curl -X GET "localhost:9200/_cat/segments"
curl -X GET "localhost:9200/_cat/segments/{index}"
curl -X GET "localhost:9200/_cat/count"
curl -X GET "localhost:9200/_cat/count/{index}"
curl -X GET "localhost:9200/_cat/recovery"
curl -X GET "localhost:9200/_cat/recovery/{index}"
curl -X GET "localhost:9200/_cat/health"
curl -X GET "localhost:9200/_cat/pending_tasks"
curl -X GET "localhost:9200/_cat/aliases"
curl -X GET "localhost:9200/_cat/aliases/{alias}"
curl -X GET "localhost:9200/_cat/thread_pool"
curl -X GET "localhost:9200/_cat/thread_pool/{thread_pools}"
curl -X GET "localhost:9200/_cat/plugins"
curl -X GET "localhost:9200/_cat/fielddata"
curl -X GET "localhost:9200/_cat/fielddata/{fields}"
curl -X GET "localhost:9200/_cat/nodeattrs"
curl -X GET "localhost:9200/_cat/repositories"
curl -X GET "localhost:9200/_cat/snapshots/{repository}"
curl -X GET "localhost:9200/_cat/templates"
```

---

### Old Notes

```sh
docker run -d -p 9200:9200 -p 9300:9300 -it -h elasticsearch --name elasticsearch elasticsearch:6.5.1
curl http://localhost:9200
docker run -d -p 5601:5601 -h kibana --name kibana --link elasticsearch:elasticsearch kibana:6.5.1
curl http://localhost:5601
docker run -h logstash --name logstash --link elasticsearch:elasticsearch -it --rm -v "$PWD":/config-dir logstash -f /config-dir/logstash.conf
```