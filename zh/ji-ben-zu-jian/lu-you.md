# **路由**

tastphp的路由是基于[tast-router](https://github.com/xujiajun/tast-router)。

在config目录下，默认有2个路由主配置，routes.yml 里面配置需要加载的路由

```
├── config
|__ ...
│   ├── routes.yml
│   └── routes_test.yml
```

配置的格式如下（例子取自src/FrontBundle/Config/routes.yml）：

```
home:
      pattern: /
      parameters:
        _controller: Front@Home::index
        methods:  [GET]
        routeName: home
```

* home 表示这个路由的key

* pattern 表示匹配的规则

* parameters 表示参数组

  * _controller 表示启用哪一个bundle下的控制器的Action
  
  * methods  表示用什么请求的方法
  
  * routeName 表示路由名称



