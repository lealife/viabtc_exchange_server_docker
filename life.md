# mac下 

docker-compose up
docker-compose ps
docker-compose stop


```
btc-kafka            start-kafka.sh                   Up      0.0.0.0:19092->9092/tcp                                                                                       
btc-mysql            docker-entrypoint.sh mysqld      Up      0.0.0.0:13306->3306/tcp, 33060/tcp                                                                            
btc-redis-master     docker-entrypoint.sh redis ...   Up      0.0.0.0:16379->6379/tcp                                                                                       
btc-redis-sentinel   /docker-entrypoint.sh            Up      0.0.0.0:26379->26379/tcp, 6379/tcp                                                                            
btc-redis-slave      docker-entrypoint.sh redis ...   Up      0.0.0.0:16380->6379/tcp                                                                                       
btc-service          /btc/start.sh                    Up      0.0.0.0:14444->4444/tcp, 0.0.0.0:17000->7000/tcp, 0.0.0.0:17316->7316/tcp, 0.0.0.0:17317->7317/tcp,           
                                                              0.0.0.0:17416->7416/tcp, 0.0.0.0:17424->7424/tcp, 0.0.0.0:18080->8080/tcp, 0.0.0.0:18081->8081/tcp,           
                                                              0.0.0.0:18091->8091/tcp                                                                                       
btc-zookeeper        /bin/sh -c /usr/sbin/sshd  ...   Up      0.0.0.0:12181->2181/tcp, 22/tcp, 2888/tcp, 3888/tcp 
```

docker container ls

已经停止的container还在, 如果要彻底删除: docker  rm $(docker ps -a -q) 

$ docker ps // 查看所有正在运行容器
$ docker stop containerId // containerId 是容器的ID

$ docker ps -a // 查看所有容器
$ docker ps -a -q // 查看所有容器ID

$ docker stop $(docker ps -a -q) //  stop停止所有容器
$ docker rm $(docker ps -a -q) //   remove删除所有容器, 彻底删除之

删除container之后, mysql里的数据会还原!!!!!!

cd db
docker build -t viabtc_exchange_server_docker_mysql .

curl  http://127.0.0.1:18080/ -d '{"method": "market.list", "params": [], "id": 1516681174}'

# 支持websocket
accessws/config.json
```
"svr": {
    "bind": [
        "tcp@0.0.0.0:7000" // 之前是"stream@/tmp/accessws.sock"
    ],
    "max_pkg_size": 102400,
    "protocol": "chat"
},
```

# 重新build via

cd btc
修改dockerfile
docker build -t viabtc_exchange_server_docker_btc .

然后
docker-compose up

# websocket测试

通过nginx代理c.com -> localhost:17000, 支持跨域

var ws = new WebSocket('ws://c.com')
ws.send('{"id":1,"method":"server.ping","params":[]}')

