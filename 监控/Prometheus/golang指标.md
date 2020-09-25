# GO参数

| 参数名                           | 参数解释                                        |
| :------------------------------- | :---------------------------------------------- |
| go_gc_duration_seconds           | GC调用持续时间的摘要                            |
| go_goroutines                    | 当前存在的goroutine数量                         |
| go_info                          | 有关Go环境的信息                                |
| go_memstats_alloc_bytes          | 已分配且仍在使用的字节数                        |
| go_memstats_alloc_bytes_total    | 已分配的总字节数，即使已释放也是如此            |
| go_memstats_buck_hash_sys_bytes  | 分析存储桶哈希表使用的字节数(标尺)              |
| go_memstats_frees_total          | 空闲总数(计数器)                                |
| go_memstats_gc_cpu_fraction      | 自程序启动以来，GC使用该程序的可用CPU时间的分数 |
| go_memstats_gc_sys_bytes         | 用于垃圾回收系统元数据的字节数                  |
| go_memstats_heap_alloc_bytes     | 已分配且仍在使用的堆字节数                      |
| go_memstats_heap_idle_bytes      | 等待使用的堆字节数                              |
| go_memstats_heap_inuse_bytes     | 正在使用的堆字节数                              |
| go_memstats_heap_objects         | 分配的对象数                                    |
| go_memstats_heap_released_bytes  | 已释放到OS的堆字节数                            |
| go_memstats_heap_sys_bytes       | 从系统获取的堆字节数                            |
| go_memstats_last_gc_time_seconds | 自1970年以来的最后一次垃圾回收的秒数            |
| go_memstats_lookups_total        | 指针查找总数                                    |
| go_memstats_mallocs_total        | malloc总数                                      |
| go_memstats_mcache_inuse_bytes   | mcache结构正在使用的字节数                      |
| go_memstats_mcache_sys_bytes     | 用于从系统获取的mcache结构的字节数              |
| go_memstats_mspan_inuse_bytes    | mspan结构使用的字节数                           |
| go_memstats_mspan_sys_bytes      | 用于从系统获取的mspan结构的字节数               |
| go_memstats_next_gc_bytes        | 下一次垃圾回收发生时的堆字节数                  |
| go_memstats_other_sys_bytes      | 用于其他系统分配的字节数                        |
| go_memstats_stack_inuse_bytes    | 堆栈分配器正在使用的字节数                      |
| go_memstats_stack_sys_bytes      | 从系统获取的用于堆栈分配器的字节数              |
| go_memstats_sys_bytes            | 从系统获取的字节数                              |
| go_threads                       | 创建的OS线程数                                  |
|                                  |                                                 |