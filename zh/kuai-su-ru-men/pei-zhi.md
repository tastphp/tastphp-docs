# 配置

> Tastphp的优先采用[Yaml](http://symfony.com/doc/current/components/yaml.html)写配置文件。YAML 是专门用来写配置文件的语言，非常简洁和强大，远比 JSON 格式方便。

### 项目配置目录如下

```
├── config
│   ├── config.yml
│   ├── example.app.yml
│   ├── example.dbs.yml
│   ├── example.migrations-db.php
│   ├── example.parameters.yml
│   ├── migrations.yml
│   ├── routes.yml
│   └── routes_test.yml
```

项目启动前，请把带有example前缀的如 `example.app.yml` copy一份 改成 `app.yml` ,关于数据库相关的配置（example.dbs.yml、example.migrations-db.php）可以先不配置

改完后变成：

```
├── config
│   ├── app.yml
│   ├── config.yml
│   ├── example.app.yml
│   ├── example.dbs.yml
│   ├── example.migrations-db.php
│   ├── example.parameters.yml
│   ├── migrations.yml
│   ├── parameters.yml
│   ├── routes.yml
│   └── routes_test.yml
```

ok 初步的配置完成。
