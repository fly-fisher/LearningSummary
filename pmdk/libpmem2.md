1. pmem2_config_new() 创建一个配置结构体，用于存储将要映射的对象的参数。
2. pmem2_source_from_fd()使用文件描述符创建源结构体实例，该实例描述用于映射的数据源。
3. pmem2_config_set_required_store_granularity()用于设置粒度。粒度必须是三个值之一：
   PMEM2_GRANULARITY_BYTE, PMEM2_GRANULARITY_CACHE_LINE, PMEM2_GRANULARITY_PAGE。
4. pmem2_map_new()根据提供的配置结构体和源结构体创建映射，在POSIX上，底层函数实际调用的是mmap。
   在底层实现中会根据源结构体算出文件实际长度，将该长度与配置结构体一起传给pmem2_config_validate_length()用于验证配置结构体中的映射长度  (由偏移量offset和length相加所得)与文件长度是否一致，即offset和length的值之和是否大于文件长度，大于返回错误。默认offset和length的值为0，不会超过文件长度，就不会报错。
   映射的文件是传入的源结构题的文件句柄fd，该值是在pmem2_source_from_fd()中赋值。
5.  pmem2_map_get_size()根据创建的映射结构体实例获取映射的长度。
6.  pmem2_map_get_address()根据创建的映射结构体实例获取映射的首地址。
7.  pmem2_get_persist_fn()从映射结构体获取持久化函数指针persist。
8.  调用持久化函数persist()持久化对应地址指定长度的数据。
9.  pmem2_map_delete() 去除映射文件，并释放映射结构体内存空间。
10.  pmem2_source_delete() 释放源结构体内存空间。
11.  pmem2_config_delete() 释放配置结构体内存空间。
