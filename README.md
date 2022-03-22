##Elasticsearch 8.1 instructions

To reset password for the elastic user, exec into the container and run `/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic`

Copy the ca cert to your local machine from `/usr/share/elasticsearch/config/certs/http_ca.crt`

REST API Format : http://host:port/[index]/[type]/[_action/id]

Validate node status with `curl --cacert http_ca.crt -u elastic https://localhost:9200` from within the container 

Check node usage and resources with `curl --cacert http_ca.crt -u elastic https://localhost:9200/_cat/nodes?v`

Enable shard `curl -X PUT --cacert http_ca.crt -u elastic https://localhost:9200/software?pretty&pretty`

Show shard status with `curl -X GET --cacert http_ca.crt -u elastic https://localhost:9200/_cat/indices?v&pretty`

Create a record `curl -X POST --cacert http_ca.crt -u elastic 'https://localhost:9200/software/_doc' -H 'Content-Type: applicjson' -d' { "name": "3dMax" }'`
 
Retrieve a record `curl -X GET --cacert http_ca.crt -u elastic https://localhost:9200/software/_search?pretty`

Retrieve record with filter `curl -X GET "localhost:9200/software/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match_all": { }
  },
  "sort": [
    {
      "@timestamp": "desc"
    }
  ]
}
'`


Retrieve records with `curl -XGET --cacert http_ca.crt -u elastic https://localhost:9200/customer/external/1?pretty&pretty`
 
