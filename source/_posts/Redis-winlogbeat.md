---
title: Redis-winlogbeat
date: 2018-07-31 20:02:47
tags:
---

### Redis 的 winlogbeat

```
###################### Winlogbeat Configuration Example ##########################

# This file is an example configuration file highlighting only the most common
# options. The winlogbeat.full.yml file from the same directory contains all the
# supported options with more comments. You can use it as a reference.
#
# You can find the full configuration reference here:
# https://www.elastic.co/guide/en/beats/winlogbeat/index.html

#======================= Winlogbeat specific options ==========================

# event_logs specifies a list of event logs to monitor as well as any
# accompanying options. The YAML data type of event_logs is a list of
# dictionaries.
#
# The supported keys are name (required), tags, fields, fields_under_root,
# forwarded, ignore_older, level, event_id, provider, and include_xml. Please
# visit the documentation for the complete details of each option.
# https://go.es.io/WinlogbeatConfig
winlogbeat.event_logs:
  - name: Application
    ignore_older: 72h
  - name: Security
  - name: System

#================================ General =====================================

# The name of the shipper that publishes the network data. It can be used to group
# all the transactions sent by a single shipper in the web interface.
#name:

# The tags of the shipper are included in their own field with each
# transaction published.
#tags: ["service-X", "web-tier"]

# Optional fields that you can specify to add additional information to the
# output.
fields:
  env: wineventlog

#================================ Outputs =====================================

#------------------------------- Redis output ----------------------------------
output.redis:
  # Boolean flag to enable or disable the output module.
  enabled: true

  # The list of Redis servers to connect to. If load balancing is enabled, the
  # events are distributed to the servers in the list. If one server becomes
  # unreachable, the events are distributed to the reachable servers only.
  hosts: ["35.221.167.254"]

  # The Redis port to use if hosts does not contain a port number. The default
  # is 6379.
  # port: 14011

  # The name of the Redis list or channel the events are published to. The
  # default is winlogbeat.
  key: vplaylog

  # The password to authenticate with. The default is no authentication.
  password: QFkXXBZkLD6MgcEL1y8l
```
