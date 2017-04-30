# 项目目录结构

### 项目目录结构如下：

```
├── LICENSE
├── README.md
├── _config.yml
├── bin
│   └── console.php
├── composer.json
├── composer.lock
├── config
│   ├── app.yml
│   ├── config.yml
│   ├── example.app.yml
│   ├── example.dbs.yml
│   ├── example.migrations-db.php
│   ├── example.parameters.yml
│   ├── migrations.yml
│   ├── parameters.yml
│   ├── routes.yml
│   └── routes_test.yml
├── docs
├── migrations
├── phpunit.xml.dist
├── src
│   ├── App
│   ├── Common
│   ├── FrontBundle
│   └── Service
├── tests
│   ├── AppTest.php
│   ├── bootstrap.php
│   ├── config
│   ├── src
│   └── web
├── var
│   ├── cache
│   └── logs
├── vendor
│   └── ...
└── web
    ├── assets
    ├── bootstrap.php
    ├── favicon.ico
    ├── index.php
    └── views
```

### 目录说明：

* bin：放命令行相关目录
* config：项目配置目录，具体配置[点击此处](pei-zhi.md)
* docs：项目说明目录
* migrations：数据库迁移相关目录
* src：项目业务逻辑目录
* tests：单元测试目录
* var：存放缓存、日志目录
* vendor：composer引进的包目录
* web：视图层目录
