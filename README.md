### 魔改版的Redis去重

bloom去重

独立的去重集合

独立的调度与去重db

项目中已稳定运行一年



### 示例:

#不清空redis队列

SCHEDULER_PERSIST = True

#使用项目中的改版redis调度队列

SCHEDULER = "XXXXX.scrapy_redis.scheduler.Scheduler"

#使用项目中的改版bloomfiler redis去重队列

DUPEFILTER_CLASS = "XXXXXX.scrapy_redis.dupefilter.RFPDupeFilter"

#使用项目中改版的queue

SCHEDULER_QUEUE_CLASS = 'XXXX.scrapy_redis.queue.PriorityQueue'

#下面是用于调度请求的配置(如有权限认证请使用URL的方式连接)

REDIS_URL = 'redis://user:@' + REDIS + ':6379?db=4'

#下面是去重队列的配置(如有权限认证请使用URL的方式连接)

DUPEFILTER_REDIS_URL = 'redis://user:@' + REDIS + ':6379?db=3'


#使用的哈希函数数，默认为6

BLOOMFILTER_HASH_NUMBER = 6

#Bloomfilter使用的Redis内存位，30表示2 ^ 30 = 128MB，默认为22 (1MB 可去重130W URL)

BLOOMFILTER_BIT = 22