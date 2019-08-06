minimum kibana config:

```yaml
kibana:
  enabled: true
  env:
    ELASTICSEARCH_HOSTS: http://elk-elasticsearch-client:9200
  plugins:
    # set to true to enable plugins installation
    enabled: true
    # set to true to remove all kibana plugins before installation
    reset: false
    # Use <plugin_name,version,url> to add/upgrade plugin
    values:
      - elastalert-kibana-plugin,1.0.3,https://github.com/bitsensor/elastalert-kibana-plugin/releases/download/1.0.3/elastalert-kibana-plugin-1.0.3-6.7.0.zip
  files:
    kibana.yml:
      elastalert-kibana-plugin:
        serverHost: ela-elastalert-api
        serverPort: 3030
      elasticsearch.hosts: http://elasticsearch:9200
      server.host: "0"
      server.name: kibana
```
