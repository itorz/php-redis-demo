## About

PHP+Redis做的轻量级MQ,仅仅用于测试说明,没有实际业务

## 概述
业务实现过程中,即便没有高并发与大流量,业务的解耦与异步化也是需要考虑实现的,此时MQ就显得很重要,中小型业务开发中,RabbitMQ就显得过重,这种业务下需要的就是一个轻量级的MQ,此时用Redis就刚刚好.
##流程
基于Redis的轻量级的MQ用到了Redis的三个特性:

* List存储类型
* BRLPOP或者BLPOP操作List
* 发布/订阅模式

大体流程是:主业务完成操作后写入消息到MQ,此时并发布消息到指定Channel,而之前已经订阅了该Channel的Worker收到消息后就去MQ获取并消费消息

## 使用

1. 配置 `register.php` 和 `worker.php` 中的数据库和Redis链接

2. 导入sql文件 `mq_user.sql`

3. 运行 `worker.php` ,订阅频道 `register_success`

```
vagrant@homestead:~/code/php-redis-mq$ php work.php
```

4. 运行 `register.php` 进行测试

```
vagrant@homestead:~/code/php-redis-mq$ php register.php [姓名] [手机号]
```

## 运行结果
