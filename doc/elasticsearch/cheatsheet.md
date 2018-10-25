# Elasticsearch Cheatsheet

| Option | Description |
|--------|-------------|
| [ELASTICSEARCH-HOST] | If you are accessing elasticsearch on same system you can use *localhost*, which assumes that you are submitting the request locally; otherwise, replace *localhost* with your node’s IP address.|
| [ELASTICSEARCH-PORT] | Default Elasticsearch port is *9200*. Please use port number on which Elasticsearch is listening |
| [UPDATE-TYPE] | Settings updated can either be *persistent* (applied across restarts) or *transient* (will not survive a full cluster restart) |
| [INDEX-NAME] | You can use *_all* for INDEX-NAME to apply for all index  |
| [DOC-TYPE] | |
| [DOC-ID] | |
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
| Check Cluster Health || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/health?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/health?pretty``||
| Get Cluster Nodes || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/nodes?v |``curl XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/nodes?v``||
| Get Cluster Settings || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings?pretty``||

## Index Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Index Recovery Status || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/recovery?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/recovery?v``||
| List Indexes || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/indices?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/indices?v``||
| Perform Synched Flush on Indexes |Run a synced flush on all indexes| http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_flush/synced |``curl -XPOST http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_flush/synced``||
| Delete Index/Document |||``curl -XDELETE  http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/[DOC-TYPE]/[DOC-ID]``||

## Shard Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| List Shards || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?v``||
| List Shard Allocation with Reason || http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?h=index,shard,prirep,state,unassigned.reason |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?h=index,shard,prirep,state,unassigned.reason``||
| Get Detailed on Shard Allocation issues |Explain why a shard is unallocated| http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/allocation/explain?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/allocation/explain?pretty``||
| Manage Number of Shard Replicas |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"number_of_replicas": [REPLICA-COUNT]}'``||
| Disable Shard Allocation |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "none"}}'``||
| Enable Shard Allocation |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "null"}}'``||
| Modify Shard Allocation Delay |||``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings' -H 'Content-Type: application/json' -d '{"settings": {"index.unassigned.node_left.delayed_timeout": "[DELAY-TIME]s"}}'``||

## Template Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| List All templates ||http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_template?pretty|``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_template?pretty``||
