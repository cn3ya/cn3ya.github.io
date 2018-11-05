---
layout: post
title:  "k8s组件"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 集群组件
| 组件                      | 说明                                                |
|:-------------------------|:---------------------------------------------------|
| kube-apiserver           | api网管                                             |
| etcd                     | 一致性Key/Value存储服务,k8s服务发现                    |
| kube-scheduler           | pod任务调度器,选择节点                                 |
| kube-controller-manager  | 集群业务逻辑,监控节点状态,服务Replication,认证授权,入口管理 |
| cloud-controller-manager | 与云服务商交互                                        |

### 节点组件
| 组件               | 说明                                          |
|:------------------|:---------------------------------------------|
| kubelet           | k8s的节点agent                                |
| kube-proxy        | 网络代理                                       |
| Container Runtime | 容器服务:Docker,rkt,runc,任意OCI 实现runtime-spec |

### 扩展组件
| 组件                           | 说明           |
|:------------------------------|:--------------|
| DNS                           | 获取所有资源类型 |
| Web UI (Dashboard)            | 集群状态        |
| Container Resource Monitoring | 获取节点信息    |
| Cluster-level Logging         |               |

### 参考
+ [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
