---
layout: post
title:  "使用AnsibleVault保存敏感信息"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 背景
在生产环境部署中,许多敏感信息如数据库登录凭证需要加妥善保存

### 加密配置文件
```
ansible-vault encrypt conf.yml
```

### 参考
+ [Ansible Vault](https://docs.ansible.com/ansible/2.6/user_guide/vault.html)
