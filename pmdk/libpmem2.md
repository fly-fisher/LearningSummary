1. pmem2_config_new() 创建一个配置结构体，用于存储将要映射的对象的参数。
2. pmem2_source_from_fd()使用文件描述符创建源结构体实例，该实例描述用于映射的数据源。
3. pmem2_config_set_required_store_granularity()用于设置粒度。粒度必须是三个值之一：
   PMEM2_GRANULARITY_BYTE, PMEM2_GRANULARITY_CACHE_LINE, PMEM2_GRANULARITY_PAGE。
4. pmem2_map_new()根据提供的配置结构体和源结构体创建映射，在POSIX上，底层函数实际调用的是mmap。
