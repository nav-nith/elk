# Elasticsearch Cheatsheet

## Cluster Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Elasticsearch Status || http://[ELASTICSEARCH-HOST]:9200 |``curl -XGET http://[ELASTICSEARCH-HOST]:9200``||
| Check Cluster Health || http://[ELASTICSEARCH-HOST]:9200/_cluster/health |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cluster/health``||
| Get Cluster Nodes || http://[ELASTICSEARCH-HOST]:9200/_cat/nodes |``curl XGET http://[ELASTICSEARCH-HOST]:9200/_cat/nodes``||
| Get Cluster Settings || http://[ELASTICSEARCH-HOST]:9200/_cluster/settings |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cluster/settings``||
| Perform Synched Flush || http://[ELASTICSEARCH-HOST]:9200/_flush/synced |``curl -XPOST "[ELASTICSEARCH-HOST]:9200/_flush/synced"``||

## Index Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Index Recovery Status || http://[ELASTICSEARCH-HOST]:9200/_cat/recovery |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/recovery"``||
| List Indexes || http://[ELASTICSEARCH-HOST]:9200/_cat/indices |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/indices``||
| Delete Index/Document |||``curl -XDELETE  http://[ELASTICSEARCH-HOST]:9200/[INDEX-NAME]/[DOC-TYPE]/[doc-id]``||

## Shard Operations
| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| List Shards || http://[ELASTICSEARCH-HOST]:9200/_cat/shards |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/shards``||
| List Shard Allocation with Reason || http://[ELASTICSEARCH-HOST]:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason``||
| Get Detailed on Shard Allocation issues || http://[ELASTICSEARCH-HOST]:9200/_cluster/allocation/explain?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cluster/allocation/explain?pretty``||
| Manage Number of Shard Replicas |||``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"number_of_replicas": [REPLICA-COUNT]}'``||
| Disable Shard Allocation |||``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "none"}}'``||
| Enable Shard Allocation Temporary |||``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "null"}}'``||
| Modify Shard Allocation Delay |||``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/[INDEX-NAME]/_settings' -H 'Content-Type: application/json' -d '{"settings": {"index.unassigned.node_left.delayed_timeout": "[DELAY-TIME]s"}}'``||

| Option | Description |
|--------|-------------|
| [ELASTICSEARCH-HOST] | |
| [UPDATE-TYPE] | Settings updated can either be *persistent* (applied across restarts) or *transient* (will not survive a full cluster restart) |
| [INDEX-NAME] | |
| [DOC-TYPE] | |
| [DELAY-TIME] | |
| [REPLICA-COUNT] | |
