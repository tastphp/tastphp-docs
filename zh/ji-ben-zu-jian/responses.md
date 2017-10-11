# HTTP Responses

Http Responses 基于 Symfony的[http_foundation](https://symfony.com/doc/current/components/http_foundation.html#response)


## 基本使用：

打开文件 `src/FrontBundle/Controller/HomeController.php`

添加代码：

```
return $this->response("response ok!");

```

最后变成类似：

```
<?php

namespace TastPHP\FrontBundle\Controller;

use TastPHP\Common\Controller;

class HomeController extends Controller
{
    public function indexAction()
    {
 //       echo "<br> indexAction ~<br>";
        return $this->response("response ok!");
//        return $this->render('home/index.html.twig');
    }
}
```

打开浏览器出现结果：

```
response ok!
```

你可以根据自己的需要进一步封装。

## 源码分析

找到 src/Common/Controller.php文件,刚才调用的response执行的方法，默认实现的是兼容PSR-7标准实现：

```
    protected function response($content = '', $status = 200, $headers = array())
    {
        $response = new Response($content, $status, $headers);

        $psr7Factory = new DiactorosFactory();
        $psrResponse = $psr7Factory->createResponse($response);

        $httpFoundationFactory = new HttpFoundationFactory();
        return $httpFoundationFactory->createResponse($psrResponse);
    }
```

当然你也可以直接用原来的HttpFoundation的response返回

```
return new Response($content, $status, $headers);
```

但是建议兼容PSR-7标准的接口。

### jsonResponse

jsonResponse用法差不多

```
 return new JsonResponse(['name1'=>'tastphp~',"name2"=>"tastphp!"]);
```

结果：

```
{"name1":"tastphp~","name2":"tastphp!"}
```

兼容PSR-7也只要模仿刚才`Controller.php`的`response`方法就可以了。
