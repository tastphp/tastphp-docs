[编辑本文](https://github.com/tastphp/tastphp-docs/edit/master/zh/kuai-su-ru-men/an-zhuang.md)

# **安装**

此教程对linux、MacOS用户友好

### 几个必要条件：

* php的环境\(php7+\)
* 已经安装composer
* 安装php的redis扩展
* 安装php的zip扩展
* 安装git
* 安装wget

#### 使用 tastphp installer 安装

### 方式1

```
$ git clone https://github.com/tastphp/tastphp-installer.git

$ cd tastphp-installer

$ composer update

$ chmod +x tastphp

$ php tastphp install
```

<img src="https://github.com/tastphp-lab/assets/blob/master/install/install-screen.gif?raw=true">


### 方式2 (shell方式)

```
$ git clone https://github.com/tastphp/tastphp-installer.git

$ cd tastphp-installer

$ chmod +x bin/tastphp.sh

$ ./bin/tastphp.sh
```

### 方式3 （用composer命令）

```
composer create-project  --prefer-dist tast-php/tast-php {your install directory} "1.3.6"
```

> tips: 如果发现composer很慢，国内用户建议使用[国内镜像](https://pkg.phpcomposer.com/)



