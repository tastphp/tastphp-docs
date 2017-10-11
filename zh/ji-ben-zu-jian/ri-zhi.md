# 日志

日志组件是基于[Monolog](https://github.com/Seldaek/monolog)

## 基本用法

打开`HomeController.php`文件，添加代码：

```
        $logger = $this->get('logger');
        $logger::info("indexAction,time:" . time());
```

最后类似：

```
<?php

namespace TastPHP\FrontBundle\Controller;

use Symfony\Component\HttpFoundation\JsonResponse;
use TastPHP\Common\Controller;

class HomeController extends Controller
{
    public function indexAction()
    {
        echo "<br> indexAction ~<br>";
        $logger = $this->get('logger');
        $logger::info("indexAction,time:" . time());
//        return new JsonResponse(['name1'=>'tastphp~',"name2"=>"tastphp!"]);
//        return $this->response("response ok!");
        return $this->render('home/index.html.twig');
    }
}
```

打开`tastphp-docs-demo/var/logs/info.log`文件，会发现多了一条类似：

```
[2017-10-11 07:41:05] tastphp.logger.INFO: indexAction,time:1507707665 [] []

```

> 默认logs文件目录`var/logs`,会根据不同的level（error、info、warning、debug、notice）生成对应的文件，例子中生成了info.log的文件


### 携带更多信息

在刚才的HomeController.php文件中增加一行代码：
```
$logger::info("indexAction,time:" . time(),['name1'=>'tastphp~',"name2"=>"tastphp!"]);//第二个参数$context（数组类型）

```

打开`tastphp-docs-demo/var/logs/info.log`文件，会发现多了一条类似：

```
[2017-10-11 07:50:17] tastphp.logger.INFO: indexAction,time:1507708217 {"name1":"tastphp~","name2":"tastphp!"} []
```

> error、warning、debug等用法和info类似。
