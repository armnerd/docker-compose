# 日志监控

## Es和kibana

> docker-compose

https://github.com/deviantony/docker-elk

## Filebeat

> 配置日志目录

```
- type: log
  enabled: true
  paths:
    - /path-to-logs/*/*.log
```

> 配置kibana

```
setup.kibana:
  host: "localhost:5601"
  username: "elastic"
  password: "changeme"
```

> 自定义index需要的配置

```
setup.template.name: "tmp"
setup.template.pattern: "tmp-*"
setup.ilm.enabled: false
```

> 配置es以及自定义的index

```
output.elasticsearch:
  hosts: ["localhost:9200"]
  username: "elastic"
  password: "changeme"
  index: "your-index"
```

> run起来

```
./filebeat -c filebeat.yml -e
```