# Command Cheatsheet:

| Operation | Browser URL | Curl Command | Descreprion |
| ----------|-------------|--------------|-------------|
| Check Elasticsearch Status | http://localhost:9200 | ``curl -XGET localhost:9200`` ||
| Check Cluster Health | http://localhost:9200/_cluster/health | ``curl -XGET localhost:9200/_cluster/health`` ||
| List Indexes | http://localhost:9200/_cat/indices | ``curl -XGET localhost:9200/_cat/indices`` ||
| List Shards | http://localhost:9200/_cat/shards | ``curl -XGET localhost:9200/_cat/shards`` ||
| List Shard Allocation with Reason | http://localhost:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason | ``curl -XGET localhost:9200/_cat/shards?h=index,shard,prirep,state,unassigned.reason`` ||
| Disable Shard Allocation | http://localhost:9200/_cluster/settings { "persistent": {"cluster.routing.allocation.enable": "none"}} | ``curl -XPUT localhost:9200/_cluster/settings { "persistent": {"cluster.routing.allocation.enable": "none"}}`` ||
| Enable Shard Allocation | http://localhost:9200/_cluster/settings { "persistent": {"cluster.routing.allocation.enable": "null"}} | ``curl -XPUT localhost:9200/_cluster/settings { "persistent": {"cluster.routing.allocation.enable": "null"}}`` ||
| Perform Synched Flush | http://localhost:9200/_flush/synced | ``curl -X POST "localhost:9200/_flush/synced"`` ||
||
