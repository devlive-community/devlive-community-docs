[TOC]


Accumulo can be tuned to improve read and write performance.

Read performance
-----------------------------------------------------------------------------------------------------

1.  Enable [caching]($Caching) on tables to reduce reads to disk.

2.  Enable [bloom filters]($Table-Configuration#bloom-filters) on tables to limit the number of disk lookups.

3.  Decrease the [major compaction ratio]($Table-Configuration#compaction) of a table to decrease the number of files per tablet. Less files reduces the latency of reads.

4.  Decrease the size of [data blocks in RFiles]($Design#rfile) by lowering [table.file.compress.blocksize]($Server-Properties-2.x#table_file_compress_blocksize) which can result in better random seek performance. However, this can increase the size of indexes in the RFile. If the indexes are too large to fit in cache, this can hinder performance. Also, as the index size increases the depth of the index tree in each file may increase. Increasing [table.file.compress.blocksize.index]($Server-Properties-2.x#table_file_compress_blocksize_index) can reduce the depth of the tree.


Write performance
-------------------------------------------------------------------------------------------------------

1.  Enable [native maps]($In-Depth-Installation#native-map) on tablet servers to prevent Java garbage collection pauses which can slow ingest.

2.  [Pre-split new tables]($Table-Configuration#pre-splitting-tables) to distribute writes across multiple tablet servers.

3.  Ingest data using [multiple clients]($High-Speed-Ingest#multiple-ingest-clients) or [bulk ingest](https://accumulo.apache.org/docs/2.x/development/high_speed_ingest#bulk-ingest) to increase ingest throughput.

4.  Increase the [major compaction ratio]($Table-Configuration#compaction) of a table to limit the number of major compactions which improves ingest performance.

5.  On large Accumulo clusters, use [multiple HDFS volumes]($Multi-Volume-Installations) to increase write performance.

6.  Change the compression format used by [blocks in RFiles]($Design#rfile) by setting [table.file.compress.type]($Server-Properties-2.x#table_file_compress_type) to `snappy`. This increases write speed at the expense of using more disk space.
