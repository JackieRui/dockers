### 1. Kafka

(1).命令行执行

```
#拉取镜像
$ docker pull zookeeper
$ docker pull wurstmeister/kafka
# 启动Zookeeper
docker run -d --name zookeeper \ 
-p 2181:2181 \ 
-v /Users/tiger/tiger-go/src/dockers/kafka/zk/data:/data \ 
-v /Users/tiger/tiger-go/src/dockers/kafka/zk/logs:/log \ 
zookeeper 
# 启动Kafka
docker run -d --name kafka --publish 9092:9092 --link zookeeper --env KAFKA_ZOOKEEPER_CONNECT=172.25.46.224:2181 --env KAFKA_ADVERTISED_HOST_NAME=172.25.46.224 --env KAFKA_ADVERTISED_PORT=9092 --env KAFKA_LOG_DIRS=/kafka/logs -v /Users/tiger/tiger-go/src/dockers/kfk/logs:/kafka/logs wurstmeister/kafka
# 进入kafka
$ docker exec -it kafka /bin/bash
# 创建查看Topic
docker exec kafka kafka-topics.sh --create --zookeeper 172.25.46.224:2181 --replication-factor 1 --partitions 1 --topic test
docker exec kafka kafka-topics.sh --list --zookeeper 172.25.46.224:2181
# 创建消息 直接在命令行输入消息即可
docker exec -it kafka kafka-console-producer.sh --broker-list 172.25.46.224:9092 --topic test
# 消费消息
docker exec -it kafka kafka-console-consumer.sh --bootstrap-server 172.25.46.224:9092 --topic test --from-beginning
```

