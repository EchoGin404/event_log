evevt_log   日志接收小工具服务端。支持windows、Linux部署
工具只做转存，不做审计！接收到的日志是什么样的，就什么样转存！！   



```
windows可以直接双击启动
```

![图片](https://github.com/EchoGin404/event_log/assets/52634247/d73d72a1-6aad-43fc-a406-2db324944e0c)

linux下直接运行

```
chmod  +x main
./main 
```

后台运行

```
nohup ./main 2>&1 &
```

![图片](https://github.com/EchoGin404/event_log/assets/52634247/13fb8fde-9f44-4b25-b0f4-b012a0a29dcd)



config.yaml 为配置文件，若目录下不存在，会自动新建

```yaml
# config.yaml

# Monitor IP address
monitor_ip: "0.0.0.0"

# Monitor port
monitor_port: 514

# Path for run logs
run_log_path: "Logs/Run"

# Path for syslog events
syslog_path: "Logs/Event"

# Maximum log file size (in bytes)
max_log_size: 20971520  # 20MB

# Heartbeat timeout (in nseconds: *m*s)
heartbeat_timeout: 180s

# Log retention days
log_retention_days: 180

# Allow connections from all IPs
allowed_all_ip: false

# Allowed IP addresses
allowed_ips:
    - 10.10.10.105

# Allowed IP ranges
allowed_ip_ranges:
    - 192.168.10.1/24
    - 10.10.10.1/24
    - 192.168.31.1/24

```

配置文件参数说明：

```
monitor_ip 		 ->> 	 监听的地址  默认就行
monitor_port 	 ->>  	监听端口  根据需要调整
run_log_path 	 ->>  	运行日志存放目录  默认就行
syslog_path  	->>  	接收到的日志存放目录  默认就行
max_log_size 	 ->>    单个日志文件存放的大小，超过该大小，进行轮滚 新建的日志文件进行存储
heartbeat_timeout  	->>    心跳时间
log_retention_days 	 ->>    日志存放多少天，超过设置天数则删除该天数之前得log文件
allowed_all_ip 		 ->>    是否接收监听所有ip接入
allowed_ips			  ->>    允许的ip   需要allowed_all_ip设置为false  与下不冲突
allowed_ip_ranges	  ->>  	 允许的ip段   需要allowed_all_ip设置为false  与上不冲突
```



日志存放路径，在当前程序Logs目录下
其中：

1.Event目录下存放接收到的日志

2.Run目录下存放的是运行日志

