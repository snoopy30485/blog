---
title: telegraf-windows
date: 2018-08-03 14:12:07
tags:
---

### windows-telegraf config

### 第 52 行加入Log檔案放置的路徑與檔案名稱、第 69 行輸入機器 IP、第 72 行輸入 datebase 名稱

```
# Telegraf configuration

# Telegraf is entirely plugin driven. All metrics are gathered from the
# declared inputs, and sent to the declared outputs.

# Plugins must be declared in here to be active.
# To deactivate a plugin, comment out the name and any variables.

# Use 'telegraf -config telegraf.conf -test' to see what metrics a config
# file would generate.

# Global tags can be specified here in key="value" format.
[global_tags]
  # dc = "us-east-1" # will tag all metrics with dc=us-east-1
  # rack = "1a"

# Configuration for telegraf agent
[agent]
  ## Default data collection interval for all inputs
  interval = "10s"
  ## Rounds collection interval to 'interval'
  ## ie, if interval="10s" then always collect on :00, :10, :20, etc.
  round_interval = true

  ## Telegraf will cache metric_buffer_limit metrics for each output, and will
  ## flush this buffer on a successful write.
  metric_buffer_limit = 1000
  ## Flush the buffer whenever full, regardless of flush_interval.
  flush_buffer_when_full = true

  ## Collection jitter is used to jitter the collection by a random amount.
  ## Each plugin will sleep for a random time within jitter before collecting.
  ## This can be used to avoid many plugins querying things like sysfs at the
  ## same time, which can have a measurable effect on the system.
  collection_jitter = "0s"

  ## Default flushing interval for all outputs. You shouldn't set this below
  ## interval. Maximum flush_interval will be flush_interval + flush_jitter
  flush_interval = "10s"
  ## Jitter the flush interval by a random amount. This is primarily to avoid
  ## large write spikes for users running a large number of telegraf instances.
  ## ie, a jitter of 5s and interval 10s means flushes will happen every 10-15s
  flush_jitter = "0s"

  ## Logging configuration:
  ## Run telegraf in debug mode
  debug = false
  ## Run telegraf in quiet mode
  quiet = false
  ## Specify the log file name. The empty string means to log to stdout.
  # 加入Log檔案放置的路徑與檔案名稱
  logfile = "D:\\Service\\telegraf\\telegraf.log"

  ## Override default hostname, if empty use os.Hostname()
  hostname = ""


###############################################################################
#                                  OUTPUTS                                    #
###############################################################################

# Configuration for influxdb server to send metrics to
[[outputs.influxdb]]
  # The full HTTP or UDP endpoint URL for your InfluxDB instance.
  # Multiple urls can be specified but it is assumed that they are part of the same
  # cluster, this means that only ONE of the urls will be written to each interval.
  # urls = ["udp://127.0.0.1:8089"] # UDP endpoint example
  # 輸入機器 IP
  urls = ["http://10.148.0.30:8086"] # required
  # The target database for metrics (telegraf will create it if not exists)
  # 輸入 datebase 名稱
  database = "telegraf" # required
  # Precision of writes, valid values are "ns", "us" (or "µs"), "ms", "s", "m", "h".
  # note: using second precision greatly helps InfluxDB compression
  precision = "s"

  ## Write timeout (for the InfluxDB client), formatted as a string.
  ## If not provided, will default to 5s. 0s means no timeout (not recommended).
  timeout = "5s"
  # username = "telegraf"
  # password = "metricsmetricsmetricsmetrics"
  # Set the user agent for HTTP POSTs (can be useful for log differentiation)
  # user_agent = "telegraf"
  # Set UDP payload size, defaults to InfluxDB UDP Client default (512 bytes)
  # udp_payload = 512


###############################################################################
#                                  INPUTS                                     #
###############################################################################

# Windows Performance Counters plugin.
# These are the recommended method of monitoring system metrics on windows,
# as the regular system plugins (inputs.cpu, inputs.mem, etc.) rely on WMI,
# which utilize more system resources.
#
# See more configuration examples at:
#   https://github.com/influxdata/telegraf/tree/master/plugins/inputs/win_perf_counters

[[inputs.win_perf_counters]]
  [[inputs.win_perf_counters.object]]
    # Processor usage, alternative to native, reports on a per core.
    ObjectName = "Processor"
    Instances = ["*"]
    Counters = [
      "% Idle Time",
      "% Interrupt Time",
      "% Privileged Time",
      "% User Time",
      "% Processor Time",
      "% DPC Time",
    ]
    Measurement = "win_cpu"
    # Set to true to include _Total instance when querying for all (*).
    IncludeTotal=true

  [[inputs.win_perf_counters.object]]
    # Disk times and queues
    ObjectName = "LogicalDisk"
    Instances = ["*"]
    Counters = [
      "% Idle Time",
      "% Disk Time",
      "% Disk Read Time",
      "% Disk Write Time",
      "Current Disk Queue Length",
      "% Free Space",
      "Free Megabytes",
    ]
    Measurement = "win_disk"
    # Set to true to include _Total instance when querying for all (*).
    #IncludeTotal=false

  [[inputs.win_perf_counters.object]]
    ObjectName = "PhysicalDisk"
    Instances = ["*"]
    Counters = [
      "Disk Read Bytes/sec",
      "Disk Write Bytes/sec",
      "Current Disk Queue Length",
      "Disk Reads/sec",
      "Disk Writes/sec",
      "% Disk Time",
      "% Disk Read Time",
      "% Disk Write Time",
    ]
    Measurement = "win_diskio"

  [[inputs.win_perf_counters.object]]
    ObjectName = "Network Interface"
    Instances = ["*"]
    Counters = [
      "Bytes Received/sec",
      "Bytes Sent/sec",
      "Packets Received/sec",
      "Packets Sent/sec",
      "Packets Received Discarded",
      "Packets Outbound Discarded",
      "Packets Received Errors",
      "Packets Outbound Errors",
    ]
    Measurement = "win_net"

  [[inputs.win_perf_counters.object]]
    ObjectName = "System"
    Counters = [
      "Context Switches/sec",
      "System Calls/sec",
      "Processor Queue Length",
      "System Up Time",
	  "Processes",
	  "Threads",
    ]
    Instances = ["------"]
    Measurement = "win_system"
    # Set to true to include _Total instance when querying for all (*).
    #IncludeTotal=false

  [[inputs.win_perf_counters.object]]
    # Example query where the Instance portion must be removed to get data back,
    # such as from the Memory object.
    ObjectName = "Memory"
    Counters = [
      "Available Bytes",
      "Cache Faults/sec",
      "Demand Zero Faults/sec",
      "Page Faults/sec",
      "Pages/sec",
      "Transition Faults/sec",
      "Pool Nonpaged Bytes",
      "Pool Paged Bytes",
      "Standby Cache Reserve Bytes",
      "Standby Cache Normal Priority Bytes",
      "Standby Cache Core Bytes",

    ]
    # Use 6 x - to remove the Instance bit from the query.
    Instances = ["------"]
    Measurement = "win_mem"
    # Set to true to include _Total instance when querying for all (*).
    #IncludeTotal=false

  [[inputs.win_perf_counters.object]]
    # Example query where the Instance portion must be removed to get data back,
    # such as from the Paging File object.
    ObjectName = "Paging File"
    Counters = [
      "% Usage",
    ]
    Instances = ["_Total"]
    Measurement = "win_swap"

  [[inputs.win_perf_counters.object]]
    # Process metrics
    ObjectName = "Process"
    Counters = [
      "% Processor Time",
      "Handle Count",
      "Private Bytes",
      "Thread Count",
      "Virtual Bytes",
      "Working Set"
      ]
    Instances = ["sqlservr"]
    Measurement = "win_proc"
    #IncludeTotal=false #Set to true to include _Total instance when querying for all (*).
	
  [[inputs.win_perf_counters.object]]
    # Process metrics
    ObjectName = "Process"
    Counters = [
      "% Processor Time",
      "Handle Count",
      "Private Bytes",
      "Thread Count",
      "Virtual Bytes",
      "Working Set"
      ]
    Instances = ["LogServer"]
    Measurement = "win_proc"
    #IncludeTotal=false #Set to true to include _Total instance when querying for all (*).
	
  [[inputs.ping]]
	##  List of urls to ping
	urls = ["10.148.0.13","35.186.145.86"] # required
	##  number of pings to send per collection (ping -c <COUNT>)
		count = 1
	##  interval, in s, at which to ping. 0 == default (ping -i <PING_INTERVAL>)
	# 	ping_interval = 1.0
	##  per-ping timeout, in s. 0 == no timeout (ping -W <TIMEOUT>)
		timeout = 1.0
	##  interface to send ping from (ping -I <INTERFACE>)
	# 	interface = ""
```