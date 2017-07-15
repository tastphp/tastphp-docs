# Controllers控制层


这一节，我将带你入门写控制层，首先，请看目录,你会找到Controller目录

```

├── bin
├── build
│   └── logs
├── config
├── docs
├── migrations
├── src
│   ├── App
│   ├── Common
│   │   ├── Config
│   │   └── Kit
│   ├── FrontBundle
│   │   ├── Config
│   │   ├── Controller   （看这里）
│   │   ├── Listener
│   │   └── Twig
│   │       └── Extension
│   └── Service
|....
```

进入Controller目录后，默认已经建了一个Controller文件，叫HomeController.php，内容如下：

```
<?php

namespace TastPHP\FrontBundle\Controller;

use TastPHP\Common\Controller;

class HomeController extends Controller
{
    public function indexAction()
    {
        return $this->render('home/index.html.twig');
    }
}

```

> 注意例子中 `indexAction`，在编写Controller方法时，要带上`Action`这个后缀

### 自己动手写个Controller控制器:FooController

#### 1 、配置路由

在实际开发中，控制器一般和路由进行配合使用

```
├── FrontBundle
│   ├── Config
│   │   ├── listeners.yml
│   │   └── routes.yml

```

找到routes.yml,默认内容如下：

```
home:
      pattern: /
      parameters:
        _controller: Front@Home::index
        methods:  [GET]
        routeName: home

```

在此基础上再添加一个配置:

```
Foo:
      pattern: /foo
      parameters:
        _controller: Front@Foo::index
        methods:  [GET]
        routeName: Foo

```

#### 2 编写Controller

在Controller目录下面创建一个PHP文件，命名为FooController.php

```
<?php

namespace TastPHP\FrontBundle\Controller;

use TastPHP\Common\Controller;

class FooController extends Controller
{
    public function indexAction()
    {
        echo "hello FooController Action ~";
    }
}

```

打开的你的浏览器，刷新之后，结果为：

```
hello FooController Action ~

```






