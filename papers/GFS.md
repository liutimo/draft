### Chunk Size

GFS默认使用64M作为chunk size。

好处如下：

1. 减少了Client 与 Master 之间的交互次数。
2. Client通过会对一个给定的Chunk执行多次操作。这样就能保持Client和ChunkServer的TCP长连接，进而降低网络负载。
3. 降低了Master维护的Metadata的数量。

缺点：

对于小文件而言，其Chunk可能只有一个，如果有较多的client操作该文件，保存该文件的chunkserver就会成为hot spots

> GFS首次被批处理系统使用时，出现了该问题，Google通过调整chunk的备份数量解决了。该场景下，一个潜在的长期解决方案是：允许client从其他client读取数据。



### MetaData

Master保存了三个主要的MetaData类型：

1. file and chunk namespace
2. the mapping from files to chunks
3. the locations of each chunk's replicas

所有的meta都保存在master的内存中。前两种类型的元数据还会持久化到磁盘(通过日志的方式)，同时，还会备份到远程机器上。































