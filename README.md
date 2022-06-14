# redis-faina
redis 热key 工具

#### 使用:

```
# reading from stdin
redis-cli -p 6490 MONITOR | head -n <NUMBER OF LINES TO ANALYZE> | ./redis-faina.py [options]

# reading a file
redis-cli -p 6490 MONITOR | head -n <...> > /tmp/outfile.txt
./redis-faina.py [options] /tmp/outfile.txt

	options:
--prefix-delimiter=...         	String to split on for delimiting prefix and rest of key, if not provided `:` is the default . --prefix-delimiter=#
--redis-version=...       			  Version of the redis server being monitored, if not provided `2.6` is the default. e.g. --redis-version=2.4
```

#### 输出结果:
```
#执行如下命令:

redis-cli  MONITOR |head -n 10000 |./redis-faina.py

Overall Stats
========================================
Lines Processed         10000         #总命令数
Commands/Sec            833.05        #QPS


Top Prefixes                          #请求最多的key前缀
========================================
fortrader               7424    (74.24%)
app-wind-wechat         474     (4.74%)
horizon                 449     (4.49%)
app                     196     (1.96%)
queues                  70      (0.70%)
manage                  12      (0.12%)
session                 4       (0.04%)
app_ai_boss             4       (0.04%)


Top Keys                             #请求最多的key
========================================
fortrader:oom:e688af7d-6d08-11ec-83d8-0a580a1e5444      1636    (16.36%)
fortrader:oom:981595ee-7f30-11ec-bdb4-0a580a1e54a0      1452    (14.52%)
fortrader:oom:e95dda19-7740-11ec-83d8-0a580a1e5444      912     (9.12%)
fortrader:oom:990a2bc3-7cb8-11ec-ba07-0a580a1e4cbd      568     (5.68%)
fortrader:oom:17a57b64-7e73-11ec-b522-0a580a1e4b1e      560     (5.60%)
fortrader:oom:36aaa112-7355-11ec-b509-0a580a1e472f      292     (2.92%)
fortrader:oom:802b4308-741c-11ec-b509-0a580a1e472f      208     (2.08%)
app:illuminate:queue:restart                            196     (1.96%)


Top Commands                      #执行命令top
========================================
get             7627    (76.27%)
EVAL            669     (6.69%)
hgetall         236     (2.36%)
GET             212     (2.12%)
LLEN            142     (1.42%)
EXPIRE          73      (0.73%)
ZADD            72      (0.72%)
HMSET           72      (0.72%)


Top Full Command                #执行命令top,完整输出(新增功能)
========================================
get fortrader:oom:e688af7d-6d08-11ec-83d8-0a580a1e5444          1636    (16.36%)
get fortrader:oom:981595ee-7f30-11ec-bdb4-0a580a1e54a0          1452    (14.52%)
get fortrader:oom:e95dda19-7740-11ec-83d8-0a580a1e5444          912     (9.12%)
EVAL None                                                       669     (6.69%)
get fortrader:oom:990a2bc3-7cb8-11ec-ba07-0a580a1e4cbd          568     (5.68%)
get fortrader:oom:17a57b64-7e73-11ec-b522-0a580a1e4b1e          560     (5.60%)
get fortrader:oom:36aaa112-7355-11ec-b509-0a580a1e472f          292     (2.92%)
get fortrader:oom:802b4308-741c-11ec-b509-0a580a1e472f          208     (2.08%)


Command Time (microsecs)        #请求响应时间分布
========================================
Median          14.0
75%             29.0
90%             362.75
99%             45193.25


Heaviest Commands (microsecs)   #最耗时的命令
========================================
get                     6148327.75
EVAL                    2968385.5
SETNX                   1518645.75
set                     303620.0
GET                     255816.25
lpop                    202168.75
ZREMRANGEBYSCORE        157942.75
SETEX                   78898.75


Slowest Calls               #慢请求
========================================
100605.0        "get" "app-wind-wechat:base-remark-task-index"
100603.75       "get" "app-wind-wechat:base-remark-task-index"
100601.0        "get" "app-wind-wechat:base-tag-task-index"
100592.0        "get" "app-wind-wechat:base-tag-task-index"
100567.0        "get" "app-wind-wechat:base-tag-task-index"
100541.75       "get" "app-wind-wechat:base-remark-task-index"
100502.0        "get" "app-wind-wechat:base-tag-task-index"
100499.0        "get" "app-wind-wechat:base-remark-task-index"
```

