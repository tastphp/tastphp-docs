## 数据库相关

关于数据层，Tastphp使用Doctrine的[DBAL](http://www.doctrine-project.org/projects/dbal.html)作为默认的数据操作组件，相比ORM，更高性能，更加的灵活。

> Tastphp默认支持数据库的主从，以及读写分离

## 使用

### 1、注册DoctrineService

在 `AppKernel` 初始化的时候，添加代码：

```
$this->registerDoctrineService();
```

### 2、配置数据库

> 在配置数据库之前，请保证你已经有对应数据库了

创建文件 `config/dbs.yml`,添加类似代码：

以下仅为文档demo测试，具体用户自己定义

```
dbs.options:
   master:
         driver: pdo_mysql
         host: 127.0.0.1
         password: 123
         user: root
         dbname: tastphp_demo
         charset: utf8mb4
   slave1:
         driver: pdo_mysql
         host: 127.0.0.1
         user: root
         password: 123
         dbname: tastphp_demo
         charset: utf8mb4
```

因为在之前的[命令行那一节](https://github.com/tastphp/tastphp-docs/blob/master/zh/qi-ta-zu-jian/ming-ling-xing.md)已经创建一张user表，这边就不在重复说明了。

### 3 编写API

这边以RESTFul风格API为例，编写一个添加user的API

####  3.1 配置路由

在目录config里面修改原来的`routes.yml`文件内容：

```
# for production
#FrontBundle:
#    resource: FrontBundle/Config/routes.yml
FrontBundle:
    resource:
        - FrontBundle/Config/routes.yml
        - FrontBundle/Config/user_routes.yml
BackBundle:
    resource: BackBundle/Config/routes.yml
```

为例便于路由管理，这边的`FrontBundle/Config/user_routes.yml`单独分出来


在目录 `src/FrontBundle/Config` 创建文件 `user_routes.yml`，添加代码

```
## RESRFul User API Demo
user_create:
      pattern: /user/add
      parameters:
        _controller: Front@User::add
        methods:  [POST,GET]
        routeName: user_create
```

####  3.2 编写业务逻辑（新增用户）

找到`src/FrontBundle/Controller`目录，创建文件`UserController.php`,内容如下：

```
<?php

namespace TastPHP\FrontBundle\Controller;

use TastPHP\Common\Controller;

class UserController extends Controller
{
    public function addAction()
    {
        $user = [];
        $user['username'] = "tastphp_user";
        $user['password'] = password_hash("tastphp_pass", PASSWORD_DEFAULT);
        $result = $this->getUserService()->addUser($user);
        if ($result) {
            echo "add ok";
        }
    }

    protected function getUserService()
    {
        return $this->registerService('User.UserService');
    }
}
```

> 这边前提执行过命令：`generate:entityService user`，不明白的回看[命令行那一节](https://github.com/tastphp/tastphp-docs/blob/master/zh/qi-ta-zu-jian/ming-ling-xing.md)


### 4、测试API

首先进入数据库`tastphp_demo`

```
mysql> use tastphp_demo
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+------------------------+
| Tables_in_tastphp_demo |
+------------------------+
| migration_versions     |
| user                   |
+------------------------+
2 rows in set (0.01 sec)

mysql> select * from user;
Empty set (0.00 sec)

```

用[httpie](https://github.com/jakubroztocil/httpie)具体测试下：


```
➜  tastphp-docs-demo git:(master) ✗ http -f POST http://tastphp-doc-demo.dev/user/add
HTTP/1.1 200 OK
Connection: keep-alive
Content-Encoding: gzip
Content-Type: text/html; charset=UTF-8
Date: Wed, 25 Oct 2017 07:47:51 GMT
Server: nginx/1.12.0
Transfer-Encoding: chunked
X-Powered-By: PHP/7.1.10

add ok
```

这个时候回去看下mysql:

```
mysql> mysql> select * from user;
ERROR 2006 (HY000): MySQL server has gone away
No connection. Trying to reconnect...
Connection id:    23
Current database: tastphp_demo

+----+--------------+--------------------------------------------------------------+
| id | username     | password                                                     |
+----+--------------+--------------------------------------------------------------+
|  1 | tastphp_user | $2y$10$vo/YQTbO/oHmedoDac2NHOnbvBRjITxI3kXPbEvoEn0hFhdIa/yxK |
+----+--------------+--------------------------------------------------------------+
1 row in set (0.05 sec)
```

发现多了一条记录，说明API执行成功！

下一节，我将带大家编写RESTFul风格的user API 完整的CRUD。
