<p align="center">
    <img height="70%" width="70%" src="https://raw.githubusercontent.com/tastphp-lab/assets/master/logo/tastphp-logo-big.png">
</p>

<p align="center">
<a href="https://travis-ci.org/tastphp/tastphp"><img src="https://api.travis-ci.org/tastphp/tastphp.svg?branch=master" alt="Build Status"></a>
<a href="https://codeclimate.com/github/tastphp/tastphp"><img src="https://codeclimate.com/github/tastphp/tastphp/badges/gpa.svg" alt="Code Climate"></a>
<a href="https://packagist.org/packages/tast-php/tast-php"><img src="https://poser.pugx.org/tast-php/tast-php/v/stable" alt="Latest Stable Version"></a>
<a href="https://img.shields.io/badge/support-psr7-brightgreen.svg"><img src="https://img.shields.io/badge/support-psr7-brightgreen.svg" alt="License"></a>
<a href="https://img.shields.io/badge/support-psr11-brightgreen.svg"><img src="https://img.shields.io/badge/support-psr11-brightgreen.svg" alt="License"></a>
<a href="https://packagist.org/packages/tast-php/tast-php"><img src="https://poser.pugx.org/tast-php/tast-php/license" alt="License"></a>
</p>

> Tastphp是一款现代化的PHP框架，具备灵活、组件化、可拔插、扩展性强、高性能的特点。


## 背景

PHP发展到现在，已经涌现出一大批优秀的框架，如Symfony、laravel等，而随着composer、psr 规范的出现。慢慢让PHP界开始有序，而不再一盘散沙似的重复造轮子。

当时我在为公司选框架的时候，我大概有这几点关心的（排名不分先后）：

```
0 现代化的
1 学习成本低
2 开发文档齐全
3 开发效率高
4 性能高
5 灵活
6 方便调试
7 少点magic
8 有人在维护的
```
当时github 上排名前三的（截止2017.10.26还是这样的结果）：

* Laravel 
* Symfony 
* CodeIgniter

首先排除CodeIgniter，之前用symfony框架，再来看CodeIgniter有种味道不对，而且不够现代化，看他的composer就知道了，现代化框架基本上组件化了。

由于之前Symfony，评价十分强大。但有点重了。

再来看laravel号称优雅的php框架。使用了下发现，性能不高，其次他的很多magic，导致我ide根本没法定位。设计过度嫌疑。至于后来出的lumen还没来得起尝试。号称性能超silex、silm等微框架。

> 对开发者来说学习时间成本可能还是最重要的

最后还是决定自己组建框架。有了现在的Tastphp。取名Tastphp，由于Tast等同于Taste[teist]，发音一样 我把e去掉了，意在表达品味php或有品位的php框架。

Tastphp为现代PHP开发人员，提供多一种选择。Tastphp不是Symfony、Laravel等框架的颠覆者。而是站在巨人肩膀上，吸取前人的优秀思想，选用优秀的组件，不断去改进，为实际开发需求而生的。

> Tastphp倡导是简单实用优雅哲学,希望给开发者更小学习框架的时间成本。把精力更好的放在业务开发上。Tastphp希望让你10分钟入门。1小时就可以进行开发！

Tastphp框架受到Symfony、Silex影响较大，也在不断借鉴别的优秀框架以及技术，希望Tastphp越来越棒。

Tastphp的产生也是在我司(杭州持码网络科技有限公司)内部孵化，经过实际生产环境的考验（生产环境千万级别以上日pv访问）。

Tastphp取之于开源界，现在反馈给开源界。有什么不足以及建议。请帮一起改进，毕竟个人精力有限。欢迎提交PR。

* tastphp骨架地址：https://github.com/tastphp/tastphp
* tastphp核心地址：https://github.com/tastphp/framework

## 特点
* 作为现代化框架，支持PSR2、PSR4、PSR7、PSR11
* DI（依赖注入机制）
* M（Service/Dao）VC 架构
* 组件化
* [高性能](https://github.com/xujiajun/php-framework-benchmark)
* 事件派发机制
* 可扩展性高
* 支持mysql读写分离
* 命令行控制台
* Debug Bar

## 性能测试

<img src="https://raw.githubusercontent.com/xujiajun/php-framework-benchmark/master/imgs/php-framework-vs.png">


👉 各个主流框架性能评测：https://github.com/xujiajun/php-framework-benchmark


> 本文档源代码托管在github上:[源代码地址](https://github.com/tastphp/tastphp-docs)
> , 你也可以直接源代码阅读本教程：[入口](https://github.com/tastphp/tastphp-docs/blob/master/zh/SUMMARY.md)

## 加群交流

QQ群 628043345  欢迎交流~

<img src="https://raw.githubusercontent.com/tastphp-lab/assets/master/imgs/tastphp-qq-qun.jpeg">



