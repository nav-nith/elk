# Elasticsearch Cheatsheet

| Option | Description |
|--------|-------------|
| [ELASTICSEARCH-HOST] | IP address of system where Elasticsearch is hosted. If you are accessing elasticsearch on same system you can use *localhost*, which assumes that you are submitting the request locally; otherwise, replace *localhost* with your server IP address.|
| [ELASTICSEARCH-PORT] | Port number on which Elasticsearch is listening. Default port is *9200* |
| [HDD-WATERMARK] | Percentage of Hard disc at which low disc allert to be raised. Value range between 1 to 99 |
| [UPDATE-TYPE] | Settings updated can either be *persistent* (applied across restarts) or *transient* (will not survive a full cluster restart) |
| [INDEX-NAME] | Name of index on which the action to be performed. You can use *_all* to apply for all index  |
| [DOC-TYPE] | *_type* system field of a document to elasticsearch. Generally the value will be of type *doc* |
| [DOC-ID] | *_id* system field of a document entry to elasticsearch. ES generates unique key for each entry unless explicitly specified |
| [DELAY-TIME] | |
| [SHARDS-COUNT]|  |
| [REPLICA-COUNT] | |

## System Operations
| Operation | Description |Browser URL | Curl Command |
| ----------|-------------|------------|--------------|
| Check Elasticsearch Status | Lists status of Elastisearch cluster with ES Version, Lucanace Version, information on compatibility with previous ES versions etc. | http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT] |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]``|
| Check Resource Utilization | List inforation on shards, disk usage, host and node ip | http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/allocation?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/allocation?v``|
| Set Low Disc Watermark | Set percentage of HDD at which low disc allert raised | Not Supported |``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d'{"transient": {"cluster.routing.allocation.disk.watermark.low": "[HDD-WATERMARK]%"}}'``|
|Set TransLog Size |Set Transaction Logs size which defines the write buffer flush |Not Supported|``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{ "index": {"translog.flush_threshold_size": "[TRANSLOG-SIZE]"}}'``|

## Cluster Operations
| Operation | Description |Browser URL | Curl Command |
| ----------|-------------|------------|--------------|
| Check Cluster Health | Provides information on Cluster health such as status, number_of_nodes, shards status, Task status etc. | http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/health?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/health?pretty``|
| Get Cluster Nodes | List information on all nodes of the cluster | http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/nodes?v |``curl XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/nodes?v``|
| Get Cluster Settings | Lists all *persistent* and *transient* settings of cluster | http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings?pretty``|

## Index Operations
| Operation | Description |Browser URL | Curl Command |
| ----------|-------------|------------|--------------|
| Check Index Recovery Status | View of index shard recoveries, both on-going and previously completed| http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/recovery?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/recovery?v``||
| List Indexes | Provides a cross-section of each index | http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/indices?v |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/indices?v``|
| Perform Synched Flush on Indexes |Run a synced flush on all indexes| http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_flush/synced |``curl -XPOST http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_flush/synced``|
| Delete Index/Document |Delete all/any specific index or documet. In case of special charecters in index name, you need to use unicode value of the same. Example: string for %{test} will be %25%7Btest%7D | Not Supported |``curl -XDELETE  http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/[DOC-TYPE]/[DOC-ID]``|
|Rename Index|Rename Index operation is done by copying index to new idex and deleteing old index.|||

## Shard Operations
| Operation | Description |Browser URL | Curl Command |
| ----------|-------------|------------|--------------|
| List Shard Allocation Status |Get list of Shards with allocation status and reason for unallocation| http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?v&h=index,shard,prirep,state,unassigned.reason |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cat/shards?v&h=index,shard,prirep,state,unassigned.reason``|
| Get Detailed on Shard Allocation issues |Explain why a shard is unallocated| http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/allocation/explain?pretty |``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/allocation/explain?pretty``|
| Manage Number of Shards per Index |Sets number of shards per index file. Default value is 5 |Not Supported|``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"number_of_shards": [SHARDS-COUNT]}'``|
| Manage Number of Shard Replicas |Set the number of replicas of shards to create across nodes. The replicas help in recovery of data in cse of any node goes down |Not Supported|``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"number_of_replicas": [REPLICA-COUNT]}'``|
| Disable Shard Allocation | Disable shard allocation to cluster. When Allocation is disabled, the index will be created for new data pushed to ES but will not be allocated to cluster. This operations helps to speedup the ES start time.|Not Supported|``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "none"}}'``|
| Enable Shard Allocation | Enables Shard Allocation to cluster to ensure new index created are searchable. For ES to work properly, you must keep this enabled|Not Supported|``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_cluster/settings -H 'Content-Type: application/json' -d '{ "[UPDATE-TYPE]": {"cluster.routing.allocation.enable": "primaries"}}'``|
| Modify Shard Allocation Delay |The allocation of replica shards which become unassigned because a node has left can be delayed with the index.unassigned.node_left.delayed_timeout dynamic setting, which defaults to 1m|Not Supported|``curl -XPUT http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"settings": {"index.unassigned.node_left.delayed_timeout": "[DELAY-TIME]s"}}'``|
|Reroute Shards|Manually migrate shards from a node to new empty primary shard|Not Supported|``curl -XPOST http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]|_cluster/reroute -H 'Content-Type: application/json' -d '{"commands": [{"allocate_empty_primary": {"index": "index - 1", "shard": [SHARDS-COUNT],"node": "[NODE-ID]","accept_data_loss": true } }] }'``|


## Template Operations
| Operation | Description |Browser URL | Curl Command |
| ----------|-------------|------------|--------------|
| List All templates ||http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_template?pretty|``curl -XGET http://[ELASTICSEARCH-HOST]:[ELASTICSEARCH-PORT]/_template?pretty``|
