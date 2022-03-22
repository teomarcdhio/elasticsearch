##Elasticsearch 8.1 instructions

To reset password for the elastic user, exec into the container and run `/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic`

Copy the ca cert to your local machine from `/usr/share/elasticsearch/config/certs/http_ca.crt`

Validate node status with `curl --cacert http_ca.crt -u elastic https://localhost:9200` from within the container 

Check node usage and resources with `curl --cacert http_ca.crt -u elastic https://localhost:9200/_cat/nodes?v`

Enable shard `curl -XPUT --cacert http_ca.crt -u elastic https://localhost:9200/customer?pretty&pretty`

Show shard status with `curl -XGET --cacert http_ca.crt -u elastic https://localhost:9200/_cat/indices?v&pretty`

Create a record with `curl -XPUT --cacert http_ca.crt -u elastic https://localhost:9200/customer/external/1?pretty&pretty -H 'Content-Type: application/json' -d'
 { "name": "Daenerys Targaryen" }'`
 
Retrieve records with `curl -XGET --cacert http_ca.crt -u elastic https://localhost:9200/customer/external/1?pretty&pretty`
 
