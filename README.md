# Yii2 assets free composer package

[![License](https://img.shields.io/github/license/laxity7/yii2-assets-free.svg)](https://github.com/laxity7/yii2-assets-free/blob/master/LICENSE)
[![Latest Stable Version](https://img.shields.io/packagist/v/laxity7/yii2-assets-free.svg)](https://packagist.org/packages/laxity7/yii2-assets-free)
[![Total Downloads](https://img.shields.io/packagist/dt/laxity7/yii2-assets-free.svg)](https://packagist.org/packages/laxity7/yii2-assets-free)

A composer package that allows you to install [yii2](https://github.com/yiisoft/yii2) without [composer-asset-plugin](https://github.com/francoispluchino/composer-asset-plugin).

## How to use?

Just require `laxity7/yii2-assets-free` instead (or after) of `yiisoft/yii2` in your `composer.json`.

## Why?

Yii2 currently depends on Asset packages to make it really easy to create frontend applications as it directly provides Widgets and Javascript/CSS components out of the box. Therefore, the [composer-asset-plugin](https://github.com/francoispluchino/composer-asset-plugin) is used which allows to
manage frontend dependencies directly in composer.json.

Sometimes however, these frontend components are not needed, e.g. if you use Yii to create a Console Application, Background workers or a REST API. So if you do not want to install the composer-asset-plugin on your production servers because you
do not need any asset functionality anyway you may use this package instead of requiring `yiisoft/yii2` directly.

## How does this work?

Magic in [composer.json](https://github.com/laxity7/yii2-assets-free/blob/2.0.0/composer.json#L9-L14)

This package claims to "[provide](https://getcomposer.org/doc/04-schema.md#provide)" the required asset packages which are only
available when composer-asset-plugin ist installed. In reallity no asset packages are installed, so this is only useful in cases [where you do not need them](#why).

## What to do with assets?
For example, to use the Debug module just add to the config

```php
'components' => [
    'assetManager' => [
        'bundles' => [
            'yii\web\JqueryAsset' => [
                'sourcePath' => null,
                'js' => [
                    '//code.jquery.com/jquery-3.4.0.min.js',
                ]
            ],
        ],
        // or like this
        //'assetMap'   => [
        //    'jquery.js' => '//code.jquery.com/jquery-3.4.0.min.js',
        //],
    ],
],
```