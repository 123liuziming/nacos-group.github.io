---
title: Nacos 概览
keywords: [nacos]
description: 什么是 Nacos？
---

# Nacos 概览

欢迎来到 Nacos 的世界！

## 什么是Nacos

Nacos `/nɑ:kəʊs/`  是 Dynamic Naming and Configuration Service的首字母简称，一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。

Nacos 致力于帮助您发现、配置和管理微服务。Nacos 提供了一组简单易用的特性集，帮助您快速实现动态服务发现、服务配置、服务元数据及流量管理。

Nacos 帮助您更敏捷和容易地构建、交付和管理微服务平台。 Nacos 是构建以**“服务”**为中心的现代应用架构 (例如微服务范式、云原生范式) 的服务基础设施。

Nacos 支持几乎所有主流类型的**“服务”**的发现、配置和管理：

- [Kubernetes Service](https://kubernetes.io/docs/concepts/services-networking/service/)
- [gRPC](https://grpc.io/docs/guides/concepts.html#service-definition)
- [Dubbo RPC Service](https://dubbo.apache.org)
- [Spring Cloud RESTful Service](https://spring.io/projects/spring-cloud)

### 产品功能

* **服务发现和服务健康监测**

  Nacos 支持基于 DNS 和基于 RPC 的服务发现。服务提供者使用 [原生SDK](./guide/user/sdk.md)、[OpenAPI](./guide/user/open-api.md)、或一个[独立的Agent](./guide/user/other-language.md)注册 Service 后，服务消费者可以使用[DNS TODO](./ecology/use-nacos-with-coredns.md) 或[HTTP&API](./guide/user/open-api.md)查找和发现服务。

  Nacos 提供对服务的实时的健康检查，阻止向不健康的主机或服务实例发送请求。Nacos 支持传输层 (PING 或 TCP)和应用层 (如 HTTP、MySQL、用户自定义）的健康检查。 对于复杂的云环境和网络拓扑环境中（如 VPC、边缘网络等）服务的健康检查，Nacos 提供了 agent 上报模式和服务端主动检测2种健康检查模式。Nacos 还提供了统一的健康检查仪表盘，帮助您根据健康状态管理服务的可用性及流量。

* **动态配置服务**

  动态配置服务可以让您以中心化、外部化和动态化的方式管理所有环境的应用配置和服务配置。

  动态配置消除了配置变更时重新部署应用和服务的需要，让配置管理变得更加高效和敏捷。

  配置中心化管理让实现无状态服务变得更简单，让服务按需弹性扩展变得更容易。

  Nacos 提供了一个简洁易用的UI ([控制台样例 Demo](http://console.nacos.io/nacos/index.html)) 帮助您管理所有的服务和应用的配置。Nacos 还提供包括配置版本跟踪、金丝雀发布、一键回滚配置以及客户端配置更新状态跟踪在内的一系列开箱即用的配置管理特性，帮助您更安全地在生产环境中管理配置变更和降低配置变更带来的风险。

* **动态 DNS 服务**

  动态 DNS 服务支持权重路由，让您更容易地实现中间层负载均衡、更灵活的路由策略、流量控制以及数据中心内网的简单DNS解析服务。动态DNS服务还能让您更容易地实现以 DNS 协议为基础的服务发现，以帮助您消除耦合到厂商私有服务发现 API 上的风险。

  Nacos 提供了一些简单的 [DNS APIs TODO](./ecology/use-nacos-with-coredns.md) 帮助您管理服务的关联域名和可用的 IP:PORT 列表.

* **服务及其元数据管理**

  Nacos 能让您从微服务平台建设的视角管理数据中心的所有服务及元数据，包括管理服务的描述、生命周期、服务的静态依赖分析、服务的健康状态、服务的流量管理、路由及安全策略、服务的 SLA 以及最首要的 metrics 统计数据。

### 产品优势

- **易于使用**
  
  Nacos经历几万人使用反馈优化，提供统一的服务发现和配置管理功能，通过直观的 Web 界面和简洁的 API，为开发和运维人员在云原生环境中带来了便捷的服务注册、发现和配置更新操作。
  
- **特性丰富**

  Nacos提供了包括服务发现、配置管理、动态 DNS 服务、服务元数据管理、流量管理、服务监控、服务治理等在内的一系列特性，帮助您在云原生时代，更轻松的构建、交付和管理微服务。
  
- **极致性能**

  Nacos经过阿里双十一超快伸缩场景的锤炼，提供高性能的服务注册和发现能力，以及低延迟的配置更新响应，确保在大规模分布式系统中的高效率和稳定运行。
  
- **超大容量**
  
  Nacos诞生自阿里的百万实例规模，造就支持海量服务和配置的管理，能够满足大型分布式系统对高并发和高可用性的需求。

- **稳定可用**

  Nacos 通过自研的同步协议，配合生态中应用广泛的Raft协议，确保了服务的高可用性和数据的稳定性，保证阿里双十一系统的高可用稳定运行。

- **开放生态**

  Nacos拥有活跃的开源社区、广泛的生态整合和持续的创新发展，不仅大量兼容了Spring Cloud、Dubbo等大受欢迎的开源框架、还提供了丰富的插件化能力，帮助用户在云原生时代，提供可定制满足自身特殊需求的独有云原生微服务系统。

## 设计理念

> 我们相信一切都是服务，每个服务节点被构想为一个星球，每个服务都是一个星系。Nacos 致力于帮助建立这些服务之间的**连接**，助力每个面向星辰的梦想能够透过云层，飞在云上，更好的链接整片星空。

Nacos希望帮助用户在云原生时代，在私有云、混合云或者公有云等所有云环境中，更好的构建、交付、管理自己的微服务平台，更快的复用和组合业务服务，更快的交付商业创新的价值，从而为用户赢得市场。正是基于这一愿景，Nacos的设计理念被定位为`易于使用`、`面向标准`、`高可用`和`方便扩展`。

![设计理念简图](/img/doc/overview/design-philosophy.svg)

#### 易于使用 

易于使用是 Nacos 的一个核心理念，它通过提供用户友好的 Web 界面和简洁的 API 来简化服务的注册、发现和配置管理过程。开发者可以轻松集成 Nacos 到他们的应用中，无需投入大量时间在复杂的设置和学习上。

#### 面向标准

Nacos 采用面向标准的设计理念，遵循云原生应用开发的最佳实践和标准协议，以确保其服务发现和配置管理功能与广泛的技术栈和平台无缝对接。

#### 高可用

为了满足企业级应用对高可用的需求，Nacos 实现了集群模式，确保在节点发生故障时，服务的发现和配置管理功能不会受影响。集群模式也意味着 Nacos 可以通过增加节点来水平扩展，提升系统的整体性能和承载能力。

![Nacos高可用架构图](/img/doc/overview/availability-structure.svg)

#### 方便扩展

Nacos 还注重易于扩展，它采用了模块化的设计使得各个组件都可以独立地进行扩展或替换。这也为社区贡献者提供了方便，使他们能够针对特定的需求开发新的功能或者改善现有功能，进一步推动 Nacos 的生态发展。

![Nacos插件架构图](/img/doc/overview/plugin-structure.svg)

通过上述设计理念的实现，Nacos 为用户提供了一个强大而灵活的平台，以支持不断变化的业务需求，加速业务创新和数字转型，最终帮助用户在竞争激烈的市场中占据有利地位。

## 部署模式

Nacos 提供了两种两种部署运行模式：`单机模式`和`集群模式`

![Nacos部署模式图](/img/doc/overview/deploy-structure.svg)

### 单机模式

单机模式又称`单例模式`, 拥有所有Nacos的功能及特性，具有极易部署、快速启动等优点。但无法与其他节点组成集群，无法在节点或网络故障时提供高可用能力。单机模式同样可以使用内置Derby数据库（默认）和外置数据库进行存储。

单机模式主要适合于工程师于本地搭建或于测试环境中搭建Nacos环境，主要用于开发调试及测试使用；也能够兼顾部分对稳定性和可用性要求不高的业务场景。

### 集群模式

集群模式通过自研一致性协议Distro以及Raft协议，将多个Nacos节点构建成了高可用的Nacos集群。数据将在集群中各个节点进行同步，保证数据的一致性。集群模式具有高可用、高扩展、高并发等优点，确保在故障发生时不影响业务的运行。集群模式**默认**采用外置数据库进行存储，但也可以通过内置数据库进行存储。

该模式主要适合于生产环境，也是社区最为推荐的部署模式。

## 生态组件

![Nacos生态图](/img/doc/overview/ecology-structure.png)

## 路线规划

![NacosRoadMap](/img/doc/overview/roadmap.svg)

## 参与社区

Nacos 主要通过Github 进行社区的协作，欢迎社区中所有的用户和开发者加入到Nacos的开发中来。详情请参考[如何共建](contribution/contributing.md)。