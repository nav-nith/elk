# Elasticsearch Cheatsheet

| Operation | Description |Browser URL | Curl Command | Responce |
| ----------|-------------|------------|--------------|----------|
| Check Elasticsearch Status || http://[ELASTICSEARCH-HOST]:9200 | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200`` ||
| Check Cluster Health || http://[ELASTICSEARCH-HOST]:9200/_cluster/health | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cluster/health`` ||
| Check Recovery Status || http://[ELASTICSEARCH-HOST]:9200/_cat/recovery | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/recovery"`` ||
| List Nodes || http://[ELASTICSEARCH-HOST]:9200/_cat/nodes | ``curl XGET http://[ELASTICSEARCH-HOST]:9200/_cat/nodes`` ||
| List Indexes || http://[ELASTICSEARCH-HOST]:9200/_cat/indices | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/indices`` ||
| List Shards || http://[ELASTICSEARCH-HOST]:9200/_cat/shards | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/shards`` ||
| List Shard Allocation with Reason || http://[ELASTICSEARCH-HOST]:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason`` ||
| Disable Shard Allocation Temporary || ``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/_cluster/settings -H 'Content-Type: application/json' -d '{ "transient": {"cluster.routing.allocation.enable": "none"}}'`` ||
| Disable Shard Allocation Permanent || ``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/_cluster/settings -H 'Content-Type: application/json' -d '{ "persistent": {"cluster.routing.allocation.enable": "none"}}'`` ||
| Enable Shard Allocation Temporary || ``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/_cluster/settings -H 'Content-Type: application/json' -d '{ "transient": {"cluster.routing.allocation.enable": "null"}}'`` ||
| Enable Shard Allocation Permanent || ``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/_cluster/settings -H 'Content-Type: application/json' -d '{ "persistent": {"cluster.routing.allocation.enable": "null"}}'`` ||
| Modify Shard Allocation Delay || ``curl -XPUT http://[ELASTICSEARCH-HOST]:9200/[INDEX-NAME]/_settings' -H 'Content-Type: application/json' -d '{"settings": {"index.unassigned.node_left.delayed_timeout": "[DELAY-TIME]s"}}'``||
| Perform Synched Flush || http://[ELASTICSEARCH-HOST]:9200/_flush/synced | ``curl -XPOST "[ELASTICSEARCH-HOST]:9200/_flush/synced"`` ||
| Get Detailed on Shard Allocation issues || http://[ELASTICSEARCH-HOST]:9200/_cluster/allocation/explain?pretty | ``curl -XGET http://[ELASTICSEARCH-HOST]:9200/_cluster/allocation/explain?pretty`` ||
| Delete Index/Document || ``curl -XDELETE  http://[ELASTICSEARCH-HOST]:9200/[INDEX-NAME]/[DOC-TYPE]/[doc-id]`` ||
| Manage Number of Shard Replicas || curl -XPUT http://[ELASTICSEARCH-HOST]:9200/[INDEX-NAME]/_settings -H 'Content-Type: application/json' -d '{"number_of_replicas": [REPLICA-COUNT]}'||

| Option | Description |
|--------|-------------|
| [ELASTICSEARCH-HOST] | |
| [INDEX-NAME] | |
| [DOC-TYPE] | |
| [DELAY-TIME] | |
| [REPLICA-COUNT] | |
