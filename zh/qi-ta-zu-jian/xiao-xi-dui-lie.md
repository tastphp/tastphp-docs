## 消息队列

Tastphp 默认用的消息队列是[beanstalkd](http://kr.github.io/beanstalkd/)

## 关于beanstalkd

job典型的生命周期

```
   put            reserve               delete
  -----> [READY] ---------> [RESERVED] --------> *poof*
```

job可能的状态迁移
```
   put with delay               release with delay
  ----------------> [DELAYED] <------------.
                        |                   |
                 kick   | (time passes)     |
                        |                   |
   put                  v     reserve       |       delete
  -----------------> [READY] ---------> [RESERVED] --------> *poof*
                       ^  ^                |  |
                       |   \  release      |  |
                       |    `-------------'   |
                       |                      |
                       | kick                 |
                       |                      |
                       |       bury           |
                    [BURIED] <---------------'
                       |
                       |  delete
                        `--------> *poof*
```

### 几个重要概念

#### Tubes
一个服务器有一个或者多个tubes，用来储存统一类型的job。每个tube由一个就绪队列与延迟队列组成。每个job所有的状态迁移在一个tube中完成。consumers消费者可以监控感兴趣的tube，通过发送watch指令。consumers消费者可以取消监控tube，通过发送ignore命令。通过watch list命令返回所有监控的tubes，当客户端预订一个job，此job可能来自任何一个它监控的tube。

#### 指令说明

* put：插入一个job到队列
* watch：说明 添加监控的tube到watch list列表，reserve指令将会从监控的tube列表获取job 
* delete：说明 从队列中删除一个job
* reserve：说明 取出（预订）job，待处理。它将返回一个新预订的job，如果没有job，beanstalkd将直到有job时才发送响应。一旦job状态迁移为reserved,取出job的client被限制在指定的时间（如果设置了ttr）完成，否则超时，job状态重装迁移为ready
* use：说明 producer生产者使用，随后使用put命令
* release：说明 release指令将一个reserved的job放回ready queue
* bury：说明 将一个job的状态迁移为buried，通过kick命令唤醒
* kick：说明 此指令应用在当前使用的tube中，它将job的状态迁移为ready或者delayed

更多信息参见 [Beanstalkd中文协议](https://github.com/kr/beanstalkd/blob/master/doc/protocol.zh-CN.md)


### 使用例子

前提安装完beanstalkd，已经启动beanstalkd


#### 1、注册

在 `AppKernel` 注册QueueService：

```
$this->registerQueueService();
```


在 `config/parameters.yml` 添加相应配置

```
beanstalkd.host: 127.0.0.1
tube: tastphpframework
```

#### 2、使用

以`HomeController`为例，在`indexAction`里面添加：

* 消息生产者：

```
$this->get('queue')->put($this->get('tube'), json_encode(['queue msg'=>"hi,tastphp framework"]));
```

* 消息消费者

`bin/queue/worker.php`里面创建文件

```
#!/usr/bin/env php
<?php
require __DIR__ . '/../../web/bootstrap.php';

$app = new \TastPHP\App\AppKernel();
$client = $app['queue']->connect();
$client->watch($app['tube']);

while ($job = $client->reserve()) {
    $received = json_decode($job->getData(), true);

    if (!empty($received)) {
        $app['logger']::info("queue job done!", $received);
        $client->delete($job);
    }
}

```

执行(这边只是测试用，线上可以用类似supervisor之类的进程管理工具)：

```
➜  tastphp-docs-demo git:(master) ✗ php bin/queue/worker.php
```

#### 结果

查看`var/logs/info.log`文件，表示成功执行：

```
[2017-10-24 16:21:44] tastphp.logger.INFO: queue job done! {"queue msg":"hi,tastphp framework"} []
```




