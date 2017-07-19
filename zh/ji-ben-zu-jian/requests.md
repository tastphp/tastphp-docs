# HTTP Requests


Http Requests 基于 Symfony的[http_foundation](https://symfony.com/doc/current/components/http_foundation.html)，Tastphp也兼容[PSR-7规范](http://www.php-fig.org/psr/psr-7/)的用法，并支持互相转换。


下面以常见的GET、POST举例子

### 基本使用

FooController 代码如下：

```
<?php

namespace TastPHP\FrontBundle\Controller;

use TastPHP\Common\Controller;
use TastPHP\Framework\Http\Request;

class FooController extends Controller
{
    public function indexAction(Request $request)
    {
        dump($request->query->get('name'));
        echo "hello FooController Action ~";
    }
}
```

访问浏览器：/foo?name=tastphp

结果返回：

```
"tastphp"
hello FooController Action ~

```

还有常用的：

```
$request->query->all();//获取所有GET值
```

POST用法 类似

```
$request->request->all();//获取所有POST值
```

### PSR-7规范的用法

把刚才的FooController的indexAction 改下

```

<?php

namespace TastPHP\FrontBundle\Controller;

use Psr\Http\Message\ServerRequestInterface;
use TastPHP\Common\Controller;

class FooController extends Controller
{
    public function indexAction(ServerRequestInterface $request)
    {
//        dump($request->query->get('name'));
//        dump($request->request->get('name'));
        dump($request);
        echo "hello FooController Action ~";
    }
}

```
结果：

```
ServerRequest {#30 ▼
  -attributes: []
  -cookieParams: []
  -parsedBody: []
  -queryParams: array:1 [▶]
  -serverParams: array:34 [▶]
  -uploadedFiles: []
  -method: "GET"
  -requestTarget: null
  -uri: Uri {#29 ▶}
  #headers: array:10 [▶]
  #headerNames: array:10 [▶]
  -protocol: "1.1"
  -stream: Stream {#27 ▶}
}
hello FooController Action ~
```
可以看到变成了ServerRequest对象。其中ServerRequest实现了ServerRequestInterface接口。

#### 获取刚才的值

```
dump($request->getQueryParams());

```
结果:

```
array:1 [▼
  "name" => "tastphp"
]
hello FooController Action ~

```

### 互相转换

```
        dump($request);
        $symfonyRequest = RequestAdapter::convertSymfonyRequest($request);
        dump($symfonyRequest);
 ```

结果：

```
ServerRequest {#30 ▼
  -attributes: []
  -cookieParams: []
  -parsedBody: []
  -queryParams: array:1 [▶]
  -serverParams: array:35 [▶]
  -uploadedFiles: []
  -method: "GET"
  -requestTarget: null
  -uri: Uri {#29 ▶}
  #headers: array:11 [▶]
  #headerNames: array:11 [▶]
  -protocol: "1.1"
  -stream: Stream {#27 ▶}
}
Request {#144 ▼
  +attributes: ParameterBag {#164 ▶}
  +request: ParameterBag {#167 ▶}
  +query: ParameterBag {#165 ▶}
  +server: ServerBag {#161 ▶}
  +files: FileBag {#162 ▶}
  +cookies: ParameterBag {#163 ▶}
  +headers: HeaderBag {#160 ▶}
  #content: ""
  #languages: null
  #charsets: null
  #encodings: null
  #acceptableContentTypes: null
  #pathInfo: null
  #requestUri: null
  #baseUrl: null
  #basePath: null
  #method: null
  #format: null
  #session: null
  #locale: null
  #defaultLocale: "en"
  -isHostValid: true
  -isClientIpsValid: true
  -isForwardedValid: true
  pathInfo: "/foo"
  requestUri: "/foo?name=tastphp"
  baseUrl: ""
  basePath: ""
  method: "GET"
  format: "html"
}
```

可以看到他们转换了。




