## 事件

Tastphp选用Symfony的组件[EventDispatcher](http://symfony.com/doc/current/components/event_dispatcher.html)来作事件订阅以及派发工作

## 例子

#### 1、 订阅事件

在主目录`config`下面创建文件`listeners.yml` ，内容：

```
front:
    resource: FrontBundle/Config/listeners.yml
```

在 `src/FrontBundle/Config` 里面创建`listeners.yml`文件

```
test.event:
  event: test.event
  listener: TastPHP\FrontBundle\Listener\TestListener
  callback: onTestAction
  priority: 0
```

#### 2、派发事件


在 `HomeController.php`的 `indexAction` 添加代码：

```
$this->get('eventDispatcher')->dispatch('test.event', new Event());
```


结果类似：

```
"onTest event action~"
```

