# 配置

### 项目配置目录如下

```
├── config
│   ├── example.app.yml
│   ├── example.dbs.yml
│   ├── example.migrations-db.php
│   ├── example.parameters.yml
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
