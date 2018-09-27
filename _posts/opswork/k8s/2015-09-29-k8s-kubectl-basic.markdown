---
layout: post
title:  "kubectl基本操作"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 常用命令

| 命令                                                                                   | 说明           |
|:--------------------------------------------------------------------------------------|:--------------|
| kubectl api-resources                                                                 | 获取所有资源类型 |
| kubectl cluster-info                                                                  | 集群状态        |
| kubectl get node                                                                      | 获取节点信息    |
| kubectl top node                                                                      | 查询节点性能参数 |
| kubectl top pod                                                                       | 查询容器性能参数 |
| kubectl config set-context $(kubectl config current-context) --namespace=istio-system | 修改默认命名空间 |
| kubectl port-forward my-pod 5000:6000                                                 | 端口转发         |

### 常用参数

| 参数                     | 说明                |
|:------------------------|:-------------------|
| --all-namespaces        | 所有命名空间         |
| -o wide                 | 显示更多信息         |
| --include-uninitialized | 显示尚未完成初始化的资源 |

### 参考
+ [kubectl Command Reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
+ [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
