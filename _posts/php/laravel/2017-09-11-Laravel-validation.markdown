---
layout: post
title:  "Laravel数据校验"
date:   2017-08-23 13:21:30
categories: Laravel
tags: PHP Laravel Validation
---

### 背景

在开发API时,经常需要对入参进行数据校验.
熟练使用laravel框架自动的数据校验功能能快速实现功能, 减少开发时间

### 内建校验规则

#### 流程

| 规则  | 说明              |
|:-----|:-----------------|
| bail | 出错不继续后面的校验 |

#### 是否为空

| 规则                                    | 说明                    |
|:---------------------------------------|:-----------------------|
| confirmed                              | 是否有*_confirmation字段 |
| filled                                 | 有不能为空               |
| nullable                               |                        |
| present                                |                        |
| required                               |                        |
| required_if:anotherfield,value,...     |                        |
| required_unless:anotherfield,value,... |                        |
| required_with:foo,bar,...              |                        |
| required_with_all:foo,bar,...          |                        |
| required_without:foo,bar,...           |                        |
| required_without_all:foo,bar,...       |                        |

#### 依赖

|                         | 说明                        |
|:------------------------|:---------------------------|
| date_equals:date        |                            |
| distinct                | `'foo.*.id' => 'distinct'` |
| gt:field                | 大于                        |
| gte:field               | 大于等于                     |
| in_array:anotherfield.* |                            |
| lt:field                |                            |
| lte:field               |                            |
| not_in:foo,bar,...      |                            |
| same:field              |                            |

#### 长度

|                         | 说明               |
|:------------------------|:------------------|
| between:min,max         | 大小处于min和max之间 |
| digits:length           |                   |
| digits_between:min,max  |                   |
| dimensions              | 图片宽高            |
| max:value               |                   |
| min:value               |                   |
| size:value              |                   |
| starts_with:foo,bar,... |                   |

#### 内容限定

|                         | 说明                                          |
|:------------------------|:---------------------------------------------|
| accepted                | `yes`,`on`,`1`,`true`                        |
| active_url              | 有A或AAAA的DNS记录                             |
| alpha                   | 字母                                          |
| alpha_dash              | 字母, 数字, 下划线                              |
| alpha_num               | 字母, 数字                                     |
| array                   | 数组                                          |
| boolean                 | `true`,  `false`, `1`, `0`, `"1"`, and `"0"` |
| date                    | 日期                                          |
| digits:length           | 数字                                          |
| email                   | 电子邮件                                       |
| file                    | 上传文件                                       |
| image                   | 是否为图片                                     |
| in:foo,bar,...          | 枚举值                                        |
| integer                 | 整型                                          |
| ip                      |                                              |
| ipv4                    |                                              |
| ipv6                    |                                              |
| json                    |                                              |
| not_in:foo,bar,...      | 不在枚举值                                     |
| not_regex:pattern       |                                              |
| numeric                 |                                              |
| regex:pattern           |                                              |
| same:field              |                                              |
| starts_with:foo,bar,... |                                              |
| string                  |                                              |
| timezone                |                                              |
| url                     |                                              |
| uuid                    |                                              |

#### 日期

| 规则                  | 说明                                                                                                  |
|:---------------------|:-----------------------------------------------------------------------------------------------------|
| after:date           | `'start_date' => 'required|date|after:tomorrow'` `'finish_date' => 'required|date|after:start_date'` |
| after_or_equal:date  |                                                                                                      |
| before:date          |                                                                                                      |
| before_or_equal:date |                                                                                                      |
| date                 |                                                                                                      |
| date_equals:date     |                                                                                                      |
| date_format:format   |                                                                                                      |


#### 文件

| 规则                      | 说明          |
|:-------------------------|:-------------|
| file                     | 上传文件       |
| image                    | 是否为图片     |
| mimetypes:text/plain,... | MIME头检查    |
| mimes:jpeg,bmp,png,...   | MIME扩展名检查 |

#### DB相关

| 规则                                 | 说明                         |
|:------------------------------------|:----------------------------|
| exists:table,column                 | 数据表talbe中字段column是否存在 |
| unique:table,column,except,idColumn |                             |

### 扩展校验规则
1. 使用规则对象

```
php artisan make:rule Uppercase
```

2. 使用闭包

```php
$validator = Validator::make($request->all(), [
    'title' => [
        'required',
        'max:255',
        function($attribute, $value, $fail) {
            if ($value === 'foo') {
                return $fail($attribute.' is invalid.');
            }
        },
    ],
]);
```

3. 扩展校验器

```php
Validator::extend('foo', function ($attribute, $value, $parameters, $validator) {
    return $value == 'foo';
});
```

### 修改局部校验错误提示信息

```php
public static $cnMessageArray = [
        'required' => ':attribute不能为空',
        'integer' => ':attribute不是整型',
        'string' => ':attribute不是字符串类型',
        'max' => [
            'numeric' => ':attribute大于最大值:max',
            'file'    => ':attribute超过最大文件限制:maxKB',
            'string'  => ':attribute超过最大长度限制:max',
            'array'   => ':attribute超过最大元素个数限制:max',
        ],
        'regex' => ':attribute不合法',
        'not_regex'  => ':attribute包含非法字符',
        'in' => ':attribute不合法',
];

$validator = app('validator')->make($metaArray, $this->validationRule, ValidationHelper::$cnMessageArray, []);
```

### 修改全局校验错误提示信息
修改`resources/lang/cn/validation.php`文件
```php
return [
    'email' => [
        'required' => '邮件格式错误',
    ],
],
```

### 参考

+ [Validation](https://laravel.com/docs/5.7/validation)
