below minimum kibana config should be applied to variables of https://github.com/helm/charts/tree/master/stable/elastic-stack :

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
    # This version should work with elastic-stack
      - elastalert-kibana-plugin,1.0.3,https://github.com/bitsensor/elastalert-kibana-plugin/releases/download/1.0.3/elastalert-kibana-plugin-1.0.3-6.7.0.zip
  # Overwrite kibana config file with elastalert-api server address
  files:
    kibana.yml:
      elastalert-kibana-plugin:
        serverHost: ela-elastalert-api
        serverPort: 3030
      # Default kibana config file content from docker immage
      elasticsearch.hosts: http://elasticsearch:9200
      server.host: "0"
      server.name: kibana
```
*Installation:* 

`helm install --debug --namespace logging -n elk stable/elastic-stack -f ./elastalert-api/elast-stack.yaml`

`git clone https://github.com/ApoXalvation/elastalert-api.git`

`helm install --debug --namespace logging -n ela ./elastalert-api -f ./elastalert-api/my-values.yaml`
