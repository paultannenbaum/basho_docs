---
title: Configure Multi Data Center Replication for Riak TS
project: riakts
version: 1.3.0+
document: guide
toc: true
index: true
keywords: [mdc, repl, configuration]
audience: advanced
---

With Riak TS 1.3, it is now possible for Basho EE customers to
replicate timeseries data between Riak clusters using Basho's
Multi-Datacenter (MDC) Replication.

## Prerequisites

* Riak TS 1.3 or later installed on two distinct clusters
    * Do not attempt to replicate timeseries data to a Riak cluster
      with Riak KV or any version of Riak TS prior to 1.3
* Basho customer *XXX no idea what phrasing to put on this*

## Configuration

### MDC

Please see *XXX link to ops/mdc/v3/configuration* for basic
configuration for MDC.

If you wish to use realtime replication for timeseries data, an
additional configuration option is required. In the `riak_repl`
section of your `advanced.config` file, add the following entry:

```advancedconfig
    {ts_realtime, true}
```

(If that is not the last entry in your `riak_repl` configuration
block, be sure to add a comma at the end of the line.)

### Tables

Each timeseries table to be replicated must be defined on each
cluster. MDC will not create new tables for you, and will compare the
data definition language on each cluster to make certain they are
equivalent before synchronization occurs.

### Turning off replication per-table

To disable realtime replication for one of your timeseries tables
while leaving the rest enabled, you can set a bucket type property
`{repl, fullsync}`. The bucket type for your timeseries table is
the same as the name of the table.

*XXX Include an HTTP example of bucket type property setting here*

To disable all replication for one of your timeseries tables, do not
create that table on the sink cluster.
