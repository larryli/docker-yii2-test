# docker-yii2-test

Build the full [Yii2](https://github.com/yiisoft/yii2) test environment base on [docker php](https://hub.docker.com/_/php/).

## PHP Version

- 7.0, 7, latest
- 5.6, 5
- 5.5

## Software

- Git
- unzip
- php intl extension
- php pdo_mysql extension
- php pdo_pgsql extension
- php gd extension
- php imagick extension
- php memcached extension
- php xdebug extension
- [Composer](https://getcomposer.org/)
- [Composer NPM/Bower Plugin](https://github.com/francoispluchino/composer-asset-plugin)
- [Codeception](http://codeception.com/) (include [PHPUnit](https://phpunit.de/))

## Extra

- Disable expose_php
- [Xdebug impact on Composer](https://getcomposer.org/xdebug)

## Use

```shell
docker pull aliyuncs.com/larryli/yii2-test
```

## Mirror on China

```shell
docker pull registry.aliyuncs.com/larryli/yii2-test
```

### Extra

- apt mirror: 
- composer mirror:

## Yii2 Test Example

Use GitLab CI and GitLab Runner with Docker

GitLab: https://gitlab.com/larryli/yii2-app-basic-example

## Source

GitHub: https://github.com/larryli/docker-yii2-test
