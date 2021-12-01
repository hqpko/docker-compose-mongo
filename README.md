# docker-compose-mongo

使用 `docker compose` 启动本地 `mongo` 集群

```
# 启动 mongo 集群
docker compose up -d

# 进入 mongo1 开始配置
docker compose exec mongo1 mongo

# 输入以下内容
rsconf = {
   _id : "rs0",
   members: [
       {
           "_id": 0,
           "host": "mongo1:27017",
           "priority": 3
       },
       {
           "_id": 1,
           "host": "mongo2:27017",
           "priority": 2
       },
       {
           "_id": 2,
           "host": "mongo3:27017",
           "priority": 1
       }
   ]
}
rs.initiate(rsconf);

# 最后需要设置下 host 
sudo echo "127.0.0.1 mongo1\n127.0.0.1 mongo2\n127.0.0.1 mongo3" >> /etc/hosts

# 现在即可通过 mongodb://localhost:27017 访问 mongo 集群，可以开始使用 mongo 事务
```