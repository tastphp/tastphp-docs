## 缓存

Tastphp默认Redis作为缓存

### 使用

#### 1、 注册服务

首先需要在 `AppKernel.php`里面 注册RedisService

```
 $this->registerRedisService();
```

#### 2、配置

找到 `config/parameters.yml` 文件添加 （根据自己的情况修改）：


```
host: 127.0.0.1
port: 6379
prefix: 'cm-china:'
auth: ''
#normal 正常| persistence 持久化
connect: persistence
```

#### 2、 测试

在`HomeController.php`的indexAction 里面 打印下：

```
dump($this->get('redis'));
```



结果类似：

```
Redis {#17 ▼
  isConnected: true
  host: "127.0.0.1"
  port: 6379
  auth: ""
  dbNum: 0
  timeout: 0.0
  persistentId: null
  options: {▶}
}

```







