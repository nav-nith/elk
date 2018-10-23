# Elasticsearch Cheatsheet

| Option | Description |
|--------|-------------|
| [ELASTICSEARCH-HOST] | If you are accessing elasticsearch on same system you can use *localhost*, which assumes that you are submitting the request locally; otherwise, replace *localhost* with your node’s IP address.|
| [ELASTICSEARCH-PORT] | Default Elasticsearch port is *9200*. Please use port number on which Elasticsearch is listening |
| [UPDATE-TYPE] | Settings updated can either be *persistent* (applied across restarts) or *transient* (will not survive a full cluster restart) |
| [INDEX-NAME] | |
| [DOC-TYPE] | |
| [DELAY-TIME] | |
| [REPLICA-COUNT] | |

## System Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Elasticsearch Status || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT] |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]``||
| Check HDD Utilization || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/allocation?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/allocation?v``||
| Set Low Disck Watermark |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d'{"transient": {"cluster.routing.allocation.disk.watermark.low": "90%"}}'``||

## Cluster Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Cluster Health || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/health |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/health``||
| Get Cluster Nodes || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/nodes |``curl XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/nodes``||
| Get Cluster Settings || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings``||

## Index Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Index Recovery Status || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/recovery |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/recovery"``||
| List Indexes || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/indices |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/indices``||
| Perform Synched Flush on Indexes || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_flush/synced |``curl -XPOST "[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_flush/synced"``||
| Delete Index/Document |||``curl -XDELETE  http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/[DOC-TYPE]/[doc-id]``||

## Shard Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| List Shards || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards``||
| List Shard Allocation with Reason || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?h=index,shard,prirep,state,unassigned.reason |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?h=index,shard,prirep,state,unassigned.reason``||
| Get Detailed on Shard Allocation issues || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/allocation/explain?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/allocation/explain?pretty``||
| Manage Number of Shard Replicas |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"number_of_replicas": [REPLICA-COUNT]}'``||
| Disable Shard Allocation |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "none"}}'``||
| Enable Shard Allocation Temporary |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "null"}}'``||
| Modify Shard Allocation Delay |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings' -H 'Content-Type: application/json' -d '{"settings": {"index.unassigned.node_left.delayed_timeout": "[DELAY-TIME]s"}}'``||

