# ps: docker-compose up

## http

* <http://localhost:9870>  hadoop
* <http://localhost:16010>  hbase
* <http://localhost:8088>  hadoop

## 启动容器后

进入hbase容器，执行/opt/hbase-1.2.6/bin/hbase-daemon.sh start thrift 连接python

## hive创建外部表

hive通过建立外部表和hbase数据库产生映射关系

*CREATE EXTERNAL TABLE* pixcelweb_article (slug string,title string,body string,author string,description string,createdAt string,updatedAt string,tags string,likes string)
*STORED BY* 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
*WITH SERDEPROPERTIES* ("hbase.columns.mapping" = ":key,a:title,a:body,a:author,a:description,a:createdAt,a:updatedAt,o:tags,o:like");

![external_table.png](external_table.png "创建外部表，hive连接hbase")

## mysql进入数据库

进入mysql容器，mysql -u root -p
pw：root

## spark 连接MySQL

将mysql-connector-java-8.0.23.jar放入docker的/opt/bitnami/spark/jars
docker inspect -f '{{.ID}}' master *查看长id*
dock cp `local path` `long id:docker path`
