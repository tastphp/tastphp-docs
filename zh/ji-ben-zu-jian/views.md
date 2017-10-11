# Views

如果你只需要用tastphp作为RestFul的Api，这一节你可以忽略。

如果你使用tastphp用作类似MVC的开发模式，请往下看。

view层，tastphp选用[Twig](https://twig.symfony.com/) 作为模板引擎。

在tastphp框架中，默认会在`web/views`和`/web/views/frontBundle`里面找模板引擎的twig文件

> Twig文档地址：https://twig.symfony.com/doc/2.x/

一般建议命名规则类似：

```
xxx.html.twig //xxx是自定义的名字，如home.html.twig
```

## 例子

### 1、View层，创建twig文件
在[tastphp-doc-demo](https://github.com/tastphp/tastphp-docs-demo)中,找到文件`tastphp-docs-demo/web/views/frontBundle/home/index.html.twig`

### 2、Controller层，编写业务代码

在[tastphp-doc-demo](https://github.com/tastphp/tastphp-docs-demo)中,找到文件`tastphp-docs-demo/src/FrontBundle/Controller/HomeController.php`,改下内容类似：

```
<?php
namespace TastPHP\FrontBundle\Controller;
use Symfony\Component\HttpFoundation\JsonResponse;
use TastPHP\Common\Controller;
class HomeController extends Controller
{
    public function indexAction()
    {
 //       echo "<br> indexAction ~<br>";
//        return new JsonResponse(['name1'=>'tastphp~',"name2"=>"tastphp!"]);
//        return $this->response("response ok!");
        return $this->render('home/index.html.twig');//这边就会去执行 web/views/frontBundle/home/index.html.twig的文件内容
    }
}
```


