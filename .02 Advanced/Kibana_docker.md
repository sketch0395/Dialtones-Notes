## Create Docker network for ElasticSearch and Kibana
``` powershell 
docker network create elastic
```

## Pull Elasticsearch Docker Image
```Powershell
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.15.1
#validate version
```

## Start Elastic container
``` Powershell
docker run --name es01 --net elastic -p 9200:9200 -it -m 1GB docker.elastic.co/elasticsearch/elasticsearch:8.15.1
```

### Generate password and enrollment token for user: Elastic
``` Powershell
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

### Pull Kibana Docker Image
``` Powershell
docker pull docker.elastic.co/kibana/kibana:8.15.1
#Validate version
```

## Start Kibana Container
``` powershell
docker run --name kib01 --net elastic -p 5601:5601 docker.elastic.co/kibana/kibana:8.15.1
```

## In Elastic Docker Container
Navigate to bin run kibana-verification-code.bat
``` Bash
bin\kibana-verification-code.bat
```