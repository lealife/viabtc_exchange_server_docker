# mac下 

docker-compose up
docker-compose ps
docker-compose stop

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

