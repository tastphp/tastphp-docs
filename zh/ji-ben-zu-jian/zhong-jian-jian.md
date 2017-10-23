# 中间件

当你需要在Request请求进入之后，到进入Controller之前，你需要一些操作，比如CSRF token 验证等。这个时候你要用到这个中间件（middleware）

## 使用

### 1、注册替换Appkernel的Middleware Listener

找到 src/App里面的 `AppKernel` 增加一行代码：

```
$this->registerMiddlewareListener(MiddlewareListener::class, "onMiddlewareAction");
```


```
<?php

namespace TastPHP\App;

use TastPHP\Framework\Event\AppEvent;
use TastPHP\Framework\Kernel;
use TastPHP\FrontBundle\Listener\MiddlewareListener;

class AppKernel extends Kernel
{
    public function __construct(array $values = [])
    {
        $this->registerMiddlewareListener(MiddlewareListener::class, "onMiddlewareAction");
        parent::__construct($values);
    }
}
```

### 2、创建自定义的MiddlewareListener

进入 src/FrontBundle/Listener 目录，创建一个Listener后缀的`MiddlewareListener.php`文件,内容如下：

```
<?php

namespace TastPHP\FrontBundle\Listener;

use TastPHP\Framework\Event\MiddlewareEvent;

class MiddlewareListener
{
    public function onMiddlewareAction(MiddlewareEvent $event)
    {
        echo "onMiddlewareAction ~";
    }
}
```

### 3、开始测试吧

打开浏览器，出现结果类似如下,说明成功：

```
onMiddlewareAction ~
indexAction ~
```
