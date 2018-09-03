---
layout: post
title:  "使用node实现id生成服务"
date:   2017-08-23 13:21:30
categories: node
tags: node id_generate
---

### 背景
在实现业务逻辑时,经常需要为新插入的数据生成id

### 实现
利用node的单线程特性,可以轻松实现数据一致性,同时node的事件驱动的非阻塞模型轻松实现高并发.
使用express框架轻松提供http类型接口
```js
Date.prototype.format = function (fmt) {
  const o = {
    "y+": this.getFullYear(),
    "M+": this.getMonth() + 1,                      //月份
    "d+": this.getDate(),                           //日
    "h+": this.getHours(),                          //小时
    "m+": this.getMinutes(),                        //分
    "s+": this.getSeconds(),                        //秒
    "q+": Math.floor((this.getMonth() + 3) / 3),    //季度
    "S+": this.getMilliseconds()                    //毫秒
  };
  for (let k in o) {
    if (new RegExp("(" + k + ")").test(fmt)){
      if(k === "y+"){
        fmt = fmt.replace(RegExp.$1, ("" + o[k]).substr(4 - RegExp.$1.length));
      }
      else if(k==="S+"){
        let lens = RegExp.$1.length;
        lens = lens === 1 ? 3 : lens;
        fmt = fmt.replace(RegExp.$1, ("00" + o[k]).substr(("" + o[k]).length - 1,lens));
      }
      else{
        fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
      }
    }
  }
  return fmt;
};

const express = require('express'),
  app = express();

const machineId = '0001';
let tokens = {},token,id,idPrefix,s;

setInterval(()=>{
  const date = new Date();
  const now = Math.round(date.getTime() / 1000);
  Object.keys(tokens).map((value) =>{
    if(value < now) {
      delete tokens[value];
    }
  });
  console.log(tokens);
},1000);

app.get('/id', (req, res) => {
  const date = new Date();
  idPrefix = date.format("yyyyMMddhhmmss") + machineId;
  s = Math.round(date.getTime() / 1000);
  if(tokens.hasOwnProperty(s)) {
    token = ++tokens[s];
  }else{
    token = tokens[s] = 1;
  }
  id = idPrefix + token.toString().padStart(18, '0');
  // console.info(id);
  res.send(id);
});

app.listen(3000, () => console.log('Service listening on port 3000!'));
```

### 对比

#### mysql自带uuid()

#### 自增

#### 有序uuid
