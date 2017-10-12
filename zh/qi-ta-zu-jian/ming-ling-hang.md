## 命令行

进到项目的主目录，执行`php bin/console`,出现console控制台操作界面：

```
➜  tastphp-docs-demo git:(master) ✗ php bin/console
  _____            _    ____   _   _  ____
 |_   _|__ _  ___ | |_ |  _ \ | | | ||  _ \
   | | / _` |/ __|| __|| |_) || |_| || |_) |
   | || (_| |\__ \| |_ |  __/ |  _  ||  __/
   |_| \__,_||___/ \__||_|    |_| |_||_|
                                             v1.3.2

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

* generate 生成一些代码模板，方便快速开发
* migrations 迁移数据库相关的操作

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
