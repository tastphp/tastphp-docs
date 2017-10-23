# CSRF

维基百科解释：


> CSRF，跨站请求伪造（英语：Cross-site request forgery），也被称为 one-click attack 或者 session riding，通常缩写为 CSRF 或者 XSRF， 是一种挟制用户在当前已登录的Web应用程序上执行非本意的操作的攻击方法


防御措施:
* 1、检查Referer字段
* 2、添加校验token

## 使用tastphp的CSRF服务组件

### 1、配置parameters.yml

进入 config文件夹，把 `parameters.yml` 默认有：

```
#csrf change it
csrf.secret: tastphp.token #自己修改密钥
csrf.ttl: 1440 #自己修改过期时间，默认1440s
```

### 2、AppKernel 注册csrfToken服务

在 `AppKernel.php`文件 添加一行：

```
$this->registerCsrfTokenService();
```

最后变成类似：

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
        $this->replaceListener(AppEvent::MIDDLEWARE,MiddlewareListener::class.'@onMiddlewareAction');
        //        $this->registerMiddlewareListener(MiddlewareListener::class, "onMiddlewareAction");
        $this->registerCsrfTokenService();
        parent::__construct($values);
    }
}
```

### 3、使用csrfToken组件

打开文件 `src/FrontBundle/Listener/MiddlewareListener.php`

#### 创建token

```
 $csrfTokenService = $event->getParameters()['csrfToken'];

```

#### 验证token

```
 $validation = $csrfTokenService->validate($token);

```

最后代码：

```
<?php

namespace TastPHP\FrontBundle\Listener;

use TastPHP\Framework\Event\MiddlewareEvent;

class MiddlewareListener
{
    public function onMiddlewareAction(MiddlewareEvent $event)
    {
        echo "onMiddlewareAction ~";

        $csrfTokenService = $event->getParameters()['csrfToken'];
        dump($csrfTokenService);

        $token = $csrfTokenService->generate();
        dump($token);  //结果 eyJpYXQiOjE1MDc2OTA0ODIsInR0bCI6MTQ0MCwiZXhwIjoxNTA3NjkxOTIyfQ.F2XPtROMM9b2JieciBwM0y7JKMBv89D6SPKzWr26w9MGpKbi_BxDGI34cf-_inBc8L5t2xKaLrxtqN_nqcUvsQ
        $validation = $csrfTokenService->validate($token);
        dump($validation); //结果 true
    }
}
```

结果：

```
onMiddlewareAction ~
CsrfTokenService {#60 ▼
  #generator: TokenGenerator {#63 ▶}
  #validator: TokenValidator {#65 ▶}
}
"eyJpYXQiOjE1MDc2OTA0ODIsInR0bCI6MTQ0MCwiZXhwIjoxNTA3NjkxOTIyfQ.F2XPtROMM9b2JieciBwM0y7JKMBv89D6SPKzWr26w9MGpKbi_BxDGI34cf-_inBc8L5t2xKaLrxtqN_nqcUvsQ"
true

indexAction ~
```

