# docker-yii2-test

基于 [docker php](https://hub.docker.com/_/php/) 构建完整的 [Yii2](https://github.com/yiisoft/yii2) 框架所需测试环境

## PHP 版本

- 7.0、7、latest
- 5.6、5
- 5.5

## 安装软件

- Git
- unzip
- php intl 扩展
- php pdo_mysql 扩展
- php pdo_pgsql 扩展
- php gd 扩展
- php imagick 扩展
- php memcached 扩展
- php xdebug 扩展
- [Composer](https://getcomposer.org/)
- [Composer NPM/Bower 插件](https://github.com/francoispluchino/composer-asset-plugin)
- [Codeception](http://codeception.com/)（含 [PHPUnit](https://phpunit.de/)）

## 额外处理

- apt-get 使用 http://mirrors.aliyun.com/ 镜像
- 关闭 expose_php
- Composer [自动禁止 xdebug](https://getcomposer.org/xdebug)
- Composer 使用 https://pkg.phpcomposer.com/ 镜像

## 使用

```shell
docker pull registry.aliyuncs.com/larryli/yii2-test
```
