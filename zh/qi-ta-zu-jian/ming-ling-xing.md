## 命令行

进到项目的主目录，执行`php bin/console`,出现console控制台操作界面：

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console
  _____            _    ____   _   _  ____
 |_   _|__ _  ___ | |_ |  _ \ | | | ||  _ \
   | | / _` |/ __|| __|| |_) || |_| || |_) |
   | || (_| |\__ \| |_ |  __/ |  _  ||  __/
   |_| \__,_||___/ \__||_|    |_| |_||_|
                                             v1.3.6

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  help                    Displays help for a command
  list                    Lists commands
 cache
  cache:config            Cache config
  cache:route             Cache route
 generate
  generate:bundle         Generates a bundle
  generate:entityService  Generates a entityService(Dao)
  generate:service        Generates a service (register into app)
 migrations
  migrations:execute      Execute a single migration version up or down manually.
  migrations:generate     Generate a blank migration class.
  migrations:latest       Outputs the latest version number
  migrations:migrate      Execute a migration to a specified version or the latest available version.
  migrations:status       View the status of a set of migrations.
  migrations:version      Manually add and delete migration versions from the version table.
```
### 说明

* cache 上线前执行，提高性能
* generate 生成一些代码模板，方便快速开发
* migrations 迁移数据库相关的操作

### cache 具体使用

#### 1、cache:config （缓存config）

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console cache:config
You have success cached config!
```

#### 2、cache:route （缓存route）

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console cache:route
You have success cached route!
```


### generate 具体使用

#### 1、generate:bundle

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console generate:bundle
Please enter the name of the bundle (default:DemoBundle):BackBundle
You have success generate BackBundleBundle
```
或者 直接执行命令 `php bin/console generate:bundle BackBundle` 效果同上，

你会发现src下多了：

```
├── BackBundle
│   ├── Config
│   ├── Controller
│   └── Listener
```

#### 2、 generate:entityService

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console generate:entityService
Please enter the name of the Entity(table name):user
You have success generate UserService(Dao)
```
或者

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console generate:entityService user
You have success generate UserService(Dao)
```

这个时候src/Service目录下自动生成User相关的Service、Dao目录以及文件模板

#### 3、generate:service 

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console generate:service
Please enter the name of service (default:demo):demo
You have success generate DemoService
```

这个时候：
```
├── App
│   └── Demo
```
src/App目录下多了一个Demo目录,Demo 目录里面多了几个文件。

```
├── Demo.php
├── DemoService.php
└── DemoServiceProvider.php
```

### migrations 具体使用

#### 生成空白的migration类，你会发现报错，如下
```
➜  tastphp-docs-demo git:(master) php bin/console migrations:generate


  [InvalidArgumentException]
  You have to specify a --db-configuration file or pass a Database Connection as a dependency to the Migrations.


migrations:generate [--editor-cmd [EDITOR-CMD]] [--configuration [CONFIGURATION]] [--db-configuration [DB-CONFIGURATION]]
```

#### 解决：配置数据库

```
在主目录的config 文件下找到 config/example.migrations-db.php 

执行cp config/example.migrations-db.php  config/migrations-db.php，也就是重新copy一份命名为migrations-db.php的php文件

```

内容如下：
```
<?php
//demo change it
return [
    'dbname'   => 'tastphp_demo', //修改数据库
    'user'     => 'root',  //修改数据库用户名
    'password' => '123',   //修改数据库密码
    'host'     => '127.0.0.1', //修改数据库host
    'driver'   => 'pdo_mysql', //修改数据库驱动
    'charset'   => 'utf8mb4' //修改数据库字符集
];
```

这个时候再执行,发现成功了：

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console migrations:generate
Loading configuration from file: migrations.yml
Generated new migration class to "/private/var/www/tastphp-docs-demo/migrations/Version20171016024937.php"
```

这个时候 migrations 目录下就有一个 `Version20171016024937.php` 文件了。

你就可以编写迁移脚本了。
这边举个例子创建一个user表，实际上你可以执行任务你自定义的SQL语句

### 具体例子

#### 1、准备的SQL

```
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(50) DEFAULT NULL,
  `password` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```

#### 2、打开刚才的文件 Version20171016024937.php

 Version20171016024937.php 内容如下：

```
<?php

namespace Migrations;

use Doctrine\DBAL\Migrations\AbstractMigration;
use Doctrine\DBAL\Schema\Schema;

/**
 * Auto-generated Migration: Please modify to your needs!
 */
class Version20171016024937 extends AbstractMigration
{
    /**
     * @param Schema $schema
     */
    public function up(Schema $schema)
    {
        // this up() migration is auto-generated, please modify it to your needs

    }

    /**
     * @param Schema $schema
     */
    public function down(Schema $schema)
    {
        // this down() migration is auto-generated, please modify it to your needs

    }
}
```

在 up 的方法里面添加第一步准备的sql语句，最后变成：

```
<?php

namespace Migrations;

use Doctrine\DBAL\Migrations\AbstractMigration;
use Doctrine\DBAL\Schema\Schema;

/**
 * Auto-generated Migration: Please modify to your needs!
 */
class Version20171016024937 extends AbstractMigration
{
    /**
     * @param Schema $schema
     */
    public function up(Schema $schema)
    {
        // this up() migration is auto-generated, please modify it to your needs
        $this->addSql("CREATE TABLE `user` (
              `id` int(11) NOT NULL AUTO_INCREMENT,
              `username` varchar(50) DEFAULT NULL,
              `password` varchar(100) DEFAULT NULL,
              PRIMARY KEY (`id`)
            ) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;"
        );
    }

    /**
     * @param Schema $schema
     */
    public function down(Schema $schema)
    {
        // this down() migration is auto-generated, please modify it to your needs

    }
}


```
查看 migrations的status：

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console migrations:status
Loading configuration from file: migrations.yml

 == Configuration

    >> Name:                                               DBAL Migrations
    >> Database Driver:                                    pdo_mysql
    >> Database Name:                                      tastphp_demo
    >> Configuration Source:                               /private/var/www/tastphp-docs-demo/config/migrations.yml
    >> Version Table Name:                                 migration_versions
    >> Version Column Name:                                version
    >> Migrations Namespace:                               Migrations
    >> Migrations Directory:                               /private/var/www/tastphp-docs-demo/migrations
    >> Previous Version:                                   Already at first version
    >> Current Version:                                    0
    >> Next Version:                                       2017-10-16 02:49:37 (20171016024937)
    >> Latest Version:                                     2017-10-16 02:49:37 (20171016024937)
    >> Executed Migrations:                                0
    >> Executed Unavailable Migrations:                    0
    >> Available Migrations:                               1
    >> New Migrations:                                     1
```

执行`migrations:migrate`

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console migrations:migrate
Loading configuration from file: migrations.yml

                    DBAL Migrations


WARNING! You are about to execute a database migration that could result in schema changes and data lost. Are you sure you wish to continue? (y/n)
Migrating up to 20171016024937 from 0

  ++ migrating 20171016024937

     -> CREATE TABLE `user` (
              `id` int(11) NOT NULL AUTO_INCREMENT,
              `username` varchar(50) DEFAULT NULL,
              `password` varchar(100) DEFAULT NULL,
              PRIMARY KEY (`id`)
            ) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;

  ++ migrated (0.11s)

  ------------------------

  ++ finished in 0.11s
  ++ 1 migrations executed
  ++ 1 sql queries
 ```
 
 这个时候你的sql已经执行，检查下刚才定义的数据库`tastphp_demo` ,你会发现多了两个表 `user`、`migration_versions`
 
 其中`migration_versions`表是管理迁移脚本的版本。
 
 ### 其他命令：
 
 #### migrations:execute 版本号
 
 ```
 php bin/console  migrations:execute 20171016024937
 ```
 
 #### migrations:latest 输出最新版本号
