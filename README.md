# Item-Seckill
如果想自己试的同学可以按照一下步骤完成配置
Support the practice of commodity kill projects under high concurrency.

# 此项目为支持高并发下的商品秒杀活动
1.使用SpringBoot框架进行开发，将项目下载之后部署到CentOs8服务器上，安装好JDK8,MySQL8，Nginx,Redis,RocketMQ

2.首先配置Nginx反向代理文件，实现服务器访问静态资源，服务器内部调用后端代码

3.将数据库上传到服务器中。配置后端代码与mysql,redis,rocketmq的连接，注意部署到服务器之后，这些都是内部调用的，网址是127.0.0.1，根据不同模块设置不同的端口连接

4.将代码打包成jar包然后上传到服务器上，利用sh文件执行代码：Linux命令：sh seckill.sh


# 由于我租的服务器，很容易被恶意侵入，前端时间被植入了挖矿程序，导致我的网站崩溃
解决方案，网站的维护很重要

入侵的主演原因：

服务器端口号默认22，用户名root;很容易入侵,所以将服务器禁止root登陆，将端口号从22改为19707，用户名：自定义,密码：自定义，登陆之后再进入root用户：su root,输入root的密码：970307Xiami;

之后将可以重启程序，要判断使用的几个组件是否启动，使用以下命令：

1.ps -ef | grep 命令

2.Nginx: 进入到/etc/nginx目录下输入nginx -s reload

3.启动nginx:   nginx -c /etc/nginx/nginx.conf

4.若显示98端口被占用：输入fuser -k 80/tcp

5.Redis: 启动redis:redis-server /etc/redis.conf

6.RocketMQ:   先进入目录cd /root/rocketmq-all-4.8.0-bin-release
```
开启nameserver:       nohup sh ./bin/mqnamesrv -n localhost:9876 &
开启broker:           nohup sh ./bin/mqbroker -n localhost:9876 -c ./conf/broker.conf &
```
			
7.关闭rocketmq:
```
关闭broker：          sh ./bin/mqshutdown broker
关闭nameserver:      sh ./bin/mqshutdown namesrv
```
      
8.mysql：查看mysql的状态：systemctl status mysqld   开启mysql:  systemctl start mysqld

9.都启动后再进入/root目录下执行sh seckill.sh可以正常访问
