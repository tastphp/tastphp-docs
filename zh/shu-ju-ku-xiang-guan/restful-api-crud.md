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

### 3、修改user

### 4、删除user

更多关于REST的概念介绍：

* https://zh.wikipedia.org/wiki/REST
* http://www.ruanyifeng.com/blog/2011/09/restful.html


