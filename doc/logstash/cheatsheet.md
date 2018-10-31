
## using environment variables if statement of logstash pipeline config
You canot directly use enviroment variables in logstash if condition. The workaround way is to assign the environment variable value to a field using mutate plugin in filter and then use the new field data in if condition.
Example:
```
input{}
filter{
  mutate {
    add_field => {"debug" => "${ENVIRONMENT_VALUE}"}
  }
}
output {
  if [ debug ] == "true"
    stdout { rubydebug{}}
    
}
```

## Copying data from Elasticsearch to Elasticsearch
