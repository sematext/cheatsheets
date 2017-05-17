## Solr Metrics API

**_Retrieving all Metrics_**

Get all metrics:

[localhost:8983/solr/admin/metrics](http://localhost:8983/solr/admin/metrics)

**_Retrieving Metrics for Specific Group_**

Metrics for a group (groups: *solr.jvm*, *solr.node*, *solr.jetty*, *solr.core.<collection_name>*):

[localhost:8983/solr/admin/metrics?group=solr.jvm](http://localhost:8983/solr/admin/metrics?group=solr.jvm)

**_Retrieving Metrics in JSON_**

Default is XML. For JSON:

[localhost:8983/solr/admin/metrics?wt=json](http://localhost:8983/solr/admin/metrics?wt=json)

[localhost:8983/solr/admin/metrics?wt=json&indent=true](http://localhost:8983/solr/admin/metrics?wt=json&indent=true)

## Jetty Metrics

**_Number _****_of_****_ Requests _****_with_****_ Given Response Status_**

Check the number of requests with the given HTTP status, useful when checking for number of errors and successful requests:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.1xx](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.1xx)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.2xx](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.2xx)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.3xx](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.3xx)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.4xx](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.4xx)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.5xx](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.5xx)

**_Aggregated Error Percentage_**

Retrieve aggregated error percentage for 1, 5 and 15 minutes periods:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-4xx-1m](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-4xx-1m)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-4xx-5m](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-4xx-5m)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-4xx-15m](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-4xx-15m)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-5xx-1m](http://)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-5xx-5m](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-5xx-1m)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-5xx-15m](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.percent-5xx-15m)

**_HTTP Requests Related Statistics_**

Statistics for all requests sent to Solr:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.requests](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.requests)

**_HTTP Method Divided Statistics_**

Statistics for a given HTTP method:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.post-requests](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.post-requests)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.put-requests](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.put-requests)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.get-requests](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.get-requests)

**_Active Requests Statistics_**

Information on current requests:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.active](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.active)

**_Asynchronous Requests Statistics_**

Asynchronous request being processed:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.async](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.async)

**_Thread Pools Utilization_**

Jetty thread pools utilization, useful for finding thread settings issues:

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.util.thread.QueuedThreadPool](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.util.thread.QueuedThreadPool)

## JVM Metrics

**_Direct Buffers Information_**

Direct buffer used by Solr that are mapped via heap memory:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=buffers.direct](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=buffers.direct)

**_Mapped Buffers Information_**

Memory mapped buffers used by Solr and shared with operating system cache:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=buffers.mapped](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=buffers.mapped)

**_Garbage Collection Information_**

Garbage collection information:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=gc](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=gc)

**_JVM Heap Statistics_**

Heap usage information:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.heap](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.heap)

**_Out Of Heap Memory Usage_**

Out of heap memory usage by Solr: 

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.non-heap](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.non-heap)

**_Memory Pools Information_**

Memory pools utilization:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.pools](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.pools)

**_Total Memory Used_**

Total memory usage of the system running Solr:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.total](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=memory.total)

**_Operating System Information_**

Operating system information (CPU count, file descriptors, swap, memory usage, load):

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=os](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=os)

**_Threads Related Statistics_**

Threads information to help checking blocked ones:

[localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=threads](http://localhost:8983/solr/admin/metrics?group=solr.jvm&prefix=threads)

## Solr Node Metrics

**_Authorization Errors_**

Authorization errors:

[localhost:8983/solr/admin/metrics?group=solr.node&prefix=ADMIN./admin/authorization.errors](http://localhost:8983/solr/admin/metrics?group=solr.node&prefix=ADMIN./admin/authorization.errors)

**_Collections API Usage Statistics_**

Collections API usage statistics:

[localhost:8983/solr/admin/metrics?group=solr.node&prefix=ADMIN./admin/collections](http://localhost:8983/solr/admin/metrics?group=solr.node&prefix=ADMIN./admin/collections)

**_ZooKeeper Communication Statistics_**

ZooKeeper communication statistics useful in diagnosing problems with connectivity:

[localhost:8983/solr/admin/metrics?group=solr.node&prefix=ADMIN./admin/zookeeper](http://localhost:8983/solr/admin/metrics?group=solr.node&prefix=ADMIN./admin/zookeeper)

**_Loaded, Unloaded & Lazy Loaded Cores_**

Information on deployed cores, working ones and lazily loaded ones:

[localhost:8983/solr/admin/metrics?group=solr.node&prefix=CONTAINER.cores](http://localhost:8983/solr/admin/metrics?group=solr.node&prefix=CONTAINER.cores)

**_Shard Handler Statistics_**

Information about shard handler, useful in diagnosing between shards communication problems:

[localhost:8983/solr/admin/metrics?group=solr.node&prefix=QUERY.httpShardHandler](http://localhost:8983/solr/admin/metrics?group=solr.node&prefix=QUERY.httpShardHandler)

**_Update Shard Handler Information_**

Update shard handler statistics to diagnose update messages transferred between shards:

[localhost:8983/solr/admin/metrics?group=solr.node&prefix=UPDATE.updateShardHandler](http://localhost:8983/solr/admin/metrics?group=solr.node&prefix=UPDATE.updateShardHandler)

## Core Or Collection Metrics

**_Update Handler Related Metrics_**

Indexing related performance information:

[localhost:8983/solr/admin/metrics?prefix=UPDATE./update](http://localhost:8983/solr/admin/metrics?prefix=UPDATE./update)

**_Transaction Log Metrics_**

Transaction log can be a source of problems if it too large, check it with:

[localhost:8983/solr/admin/metrics?prefix=TLOG](http://localhost:8983/solr/admin/metrics?prefix=TLOG)

**_Replication Statistics_**

[localhost:8983/solr/admin/metrics?prefix=REPLICATION](http://localhost:8983/solr/admin/metrics?prefix=REPLICATION)

**_Searcher Warmup And Creation Time Information_**

[localhost:8983/solr/admin/metrics?prefix=SEARCHER](http://localhost:8983/solr/admin/metrics?prefix=SEARCHER)

**_Default /select Handler Query Related Statistics_**

We can retrieve statistics about any handler, just like the default */select* handler:

[localhost:8983/solr/admin/metrics?prefix=QUERY./select](http://localhost:8983/solr/admin/metrics?prefix=QUERY./select)

**_Merges Related Information_**

Merging can be expensive or slow, check its performance with:

[localhost:8983/solr/admin/metrics?prefix=INDEX.merge](http://localhost:8983/solr/admin/metrics?prefix=INDEX.merge)

**_General Reads And Writes Information_**

All I/O operations in Solr are done via the *Directory* interface, check its usage with:

[localhost:8983/solr/admin/metrics?prefix=DIRECTORY](http://localhost:8983/solr/admin/metrics?prefix=DIRECTORY)

## Troubleshooting

**_Checking Solr memory usage_**

[localhost:8983/solr/admin/metrics?prefix=memory.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=memory.&wt=json&indent=true)

**_Garbage collection issues_**

[localhost:8983/solr/admin/metrics?prefix=gc.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=gc.&wt=json&indent=true)

[localhost:8983/solr/admin/metrics?prefix=memory.pools.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=memory.pools.&wt=json&indent=true)

**_I/O issues _**

[localhost:8983/solr/admin/metrics?prefix=DIRECTORY.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=DIRECTORY.&wt=json&indent=true)

[localhost:8983/solr/admin/metrics?prefix=INDEX.merge.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=INDEX.merge.&wt=json&indent=true)

[localhost:8983/solr/admin/metrics?prefix=INDEX.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=INDEX.&wt=json&indent=true)

**_Retrieving transaction log information _**

[localhost:8983/solr/admin/metrics?prefix=TLOG.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=TLOG.&wt=json&indent=true)

**_Checking direct and mapped memory size_**

[localhost:8983/solr/admin/metrics?prefix=buffers.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=buffers.&wt=json&indent=true)

**_Checking number of errors_**

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.4xx-responses&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.4xx-responses&wt=json&indent=true)

[localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.5xx-responses&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=org.eclipse.jetty.server.handler.DefaultHandler.5xx-responses&wt=json&indent=true)

**_Checking replication metrics_**

[localhost:8983/solr/admin/metrics?prefix=REPLICATION.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=REPLICATION.&wt=json&indent=true)

**_Retrieving searchers warm-up times_**

[localhost:8983/solr/admin/metrics?prefix=SEARCHER.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=SEARCHER.&wt=json&indent=true)

**_Threads related statistics_**

[localhost:8983/solr/admin/metrics?prefix=threads.&wt=json&indent=true](http://localhost:8983/solr/admin/metrics?prefix=threads.&wt=json&indent=true)

