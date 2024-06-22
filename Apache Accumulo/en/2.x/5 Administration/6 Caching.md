[TOC]

Accumulo [tablet servers]($Design#tablet-server-1) have **block caches** that buffer data in memory to limit reads from disk. This caching has the following benefits:

*   reduces latency when reading data
*   helps alleviate hotspots in tables

Each tablet server has an index and data block cache that is shared by all hosted tablets (see the [tablet server diagram](https://accumulo.apache.org/docs/2.x/getting-started/design#tablet-server-1) to learn more). A typical Accumulo read operation will perform a binary search over several index blocks followed by a linear scan of one or more data blocks. If these blocks are not in a cache, they will need to be retrieved from [RFiles](https://accumulo.apache.org/docs/2.x/getting-started/design#rfile) in HDFS. While the index block cache is enabled for all tables, the data block cache has to be enabled for a table by the user. It is typically only enabled for tables where read performance is critical.

Configuration
------------------------------------------------------------------------------------------

The [tserver.cache.manager.class]($Server-Properties-2.x#tserver_cache_manager_class) property controls which block cache implementation is used within the tablet server. Users can supply their own implementation and set custom configuration properties to control its behavior (see org.apache.accumulo.core.spi.cache.BlockCacheManager$Configuration.java).

The index and data block caches are configured for tables by the following properties:

*   [table.cache.block.enable]($Server-Properties-2.x#table_cache_block_enable) - enables data block cache on the table (default is `false`)
*   [table.cache.index.enable]($Server-Properties-2.x#table_cache_index_enable) - enables index block cache on the table (default is `true`)

While the index block cache is enabled by default for all Accumulo tables, users must enable the data block cache by setting [table.cache.block.enable]($Server-Properties-2.x#table_cache_block_enable) to `true` in the shell:

```
config -t mytable -s table.cache.block.enable=true
```

Or programmatically using [TableOperations.setProperty()](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/TableOperations.html#setProperty-java.lang.String-java.lang.String-java.lang.String-):

```
client.tableOperations().setProperty("mytable", "table.cache.block.enable", "true");
```

The size of the index and data block caches (which are shared by all tablets of tablet server) can be changed from their defaults by setting the following properties:

*   [tserver.cache.data.size]($Server-Properties-2.x#tserver_cache_data_size)
*   [tserver.cache.index.size]($Server-Properties-2.x#tserver_cache_index_size)
