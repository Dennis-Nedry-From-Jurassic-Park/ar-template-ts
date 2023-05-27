Windows:

```bash
docker network create -d bridge atr
```
# exec server
```bash
docker run -d \
  --name clickhouse_host \ 
  --ulimit nofile=262144:262144 \
  -p 8123:8123 \
  -v \\wsl$\Ubuntu\clickhouse_data\log:/var/log/clickhouse-server \
  -v \\wsl$\Ubuntu\clickhouse_data\data:/var/lib/clickhouse \
  clickhouse/clickhouse-server:23.1.3.5-alpine
```
# exec client
```shell
docker run -it --net=atr --rm --link clickhouse_host:clickhouse-server clickhouse/clickhouse-client:21.3.20.1 --host clickhouse-server
```