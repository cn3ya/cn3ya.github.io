---
layout: post
title:  "Laravel使用复杂sql获取模型实例"
date:   2017-08-23 13:21:30
categories: Laravel
tags: PHP Laravel ORM
---

### 背景
Laravel框架实现的ORM能有效的提高开发效率,当业务场景越来越复杂,简单的find和where查询方式获取模型实例的方法不能满足业务的需求

### 实现
使用`\Illuminate\Database\Eloquent\Builder`类的`fromQuery`方法,可以实现通过复杂查询sql获取模型的需要
{% highlight php %}
    $client = $webapp->client;
    $clientArray = explode(',',$client);
    foreach ($clientArray as &$item) {
        $item = "FIND_IN_SET('{$item}', client)";
    }
    $clientString = implode(' and ',$clientArray);
    $sql=<<<SQL
        select
        b.*,
        -- 获取最新版本
        SUBSTRING_INDEX(
            GROUP_CONCAT(
                b.version
                ORDER BY
                b.created_on DESC
            ),
            ',',
            1
        ) as version
        from webapp_component as a
        join webapp_component_ver as b on b.component_id = a.id
        where {$clientString} and a.package_id='{$componentPackage->id}'
        group by a.name,a.group_id,a.title,a.is_share,a.is_hook
        order by a.name
SQL;
    return ComponentVersionModel::fromQuery($sql);
{% endhighlight %}
