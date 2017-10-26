## RESTful API （CRUD）

关于REST，看下维基百科的介绍：

```
REST（英文：Representational State Transfer，又称具象状态传输）是Roy Thomas Fielding博士于2000年在他的博士论文[1] 中提出来的一种万维网软件架构风格，目的是便于不同软件/程序在网络（例如互联网）中互相传递信息。
```


> GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源。


### 设计RESTFul风格路由


#### 1、标准方式

标准方式主要是通过方法来区分资源的动作


```
POST /user
GET /user/{id}
DELETE /user
PUT /user
```

#### 2、非标准方式

这种方式在实战中用的比较多，这样的路由比较好区分，但注意这不是标准的RESTful风格

```
POST /user/add
GET /user/{id}
DELETE /user/remove
PUT /user/update
```

这边为了区分路由，我们例子采用非标准的方式设计路由。


### 1、增加user

这个我们在[上一节](https://github.com/tastphp/tastphp-docs/blob/master/zh/shu-ju-ku-xiang-guan.md)已经完成了

### 2、查看user

#### 2.1 配置路由

在 src/FrontBundle/Config/user_routes.yml 添加：

```
user_get:
      pattern: /user/{id}
      parameters:
        _controller: Front@User::get
        methods:  [GET]
        routeName: user_get
        id: \d+
```

#### 2.2 添加方法

在`UserController.php` 的类中增加方法：

```
    public function getAction($id)
    {
        $result = $this->getUserService()->getUser($id);
        if ($result) {
            dump($result);
        }
    }
```

#### 2.3 测试API

```
➜  tastphp-docs-demo git:(master) ✗ http -f GET http://tastphp-doc-demo.dev/user/1
HTTP/1.1 200 OK
Connection: keep-alive
Content-Encoding: gzip
Content-Type: text/html; charset=UTF-8
Date: Thu, 26 Oct 2017 04:44:40 GMT
Server: nginx/1.12.0
Transfer-Encoding: chunked
X-Powered-By: PHP/7.1.10

array(3) {
  ["id"]=>
  string(1) "1"
  ["username"]=>
  string(12) "tastphp_user"
  ["password"]=>
  string(60) "$2y$10$vo/YQTbO/oHmedoDac2NHOnbvBRjITxI3kXPbEvoEn0hFhdIa/yxK"
}
```

### 3、修改user

#### 3.1 配置路由

在 src/FrontBundle/Config/user_routes.yml 添加：

```
user_update:
      pattern: /user/update
      parameters:
        _controller: Front@User::update
        methods:  [PUT]
        routeName: user_update
```
#### 3.2 添加方法

在`UserController.php` 的类中增加方法：

```
    public function updateAction(Request $request)
    {
        $data = $request->request->all();
        $updateUser = [];
        if (!empty($id = $data['id']) && !empty($userName = $data['name'])) {
            $updateUser['username'] = $userName;
            $result = $this->getUserService()->updateUser($id, $updateUser);
            var_dump($result);
        }

    }
```
#### 3.3 测试API

```
➜  tastphp-docs-demo git:(master) ✗ http -f PUT http://tastphp-doc-demo.dev/user/update {id=1,name='tastphp_user_001'}
HTTP/1.1 200 OK
Connection: keep-alive
Content-Encoding: gzip
Content-Type: text/html; charset=UTF-8
Date: Thu, 26 Oct 2017 06:12:50 GMT
Server: nginx/1.12.0
Transfer-Encoding: chunked
X-Powered-By: PHP/7.1.10

array(3) {
  ["id"]=>
  string(1) "1"
  ["username"]=>
  string(16) "tastphp_user_001"
  ["password"]=>
  string(60) "$2y$10$vo/YQTbO/oHmedoDac2NHOnbvBRjITxI3kXPbEvoEn0hFhdIa/yxK"
}
```

### 4、删除user

更多关于REST的概念介绍：

* https://zh.wikipedia.org/wiki/REST
* http://www.ruanyifeng.com/blog/2011/09/restful.html


