---
title: Nacos 0.6�汾������֧��Dubbo��̬����֧��Docker����
keywords: nacos0.6,dubbo,docker
description: Nacos 0.6�汾������֧��Dubbo��̬����֧��Docker����
---
# Dubbo Nacos ���� v0.8.0 PRE-GA�汾����ȫ�ȶ�������

����Ͱ�΢����Դ��Ŀ?[Dubbo Nacos](https://github.com/alibaba/nacos)? �ڱ��ܷ���?**v0.8.0**?**PRE-GA**�汾�����ڳ��������Road Mapһ����Ҫ����̱��汾����һ���ɰ�ȫ�������İ汾���ر��л��ǰ�������������ϳ���Nacos�Ŀͻ��������ᾡ��ĳ�С��Ʒ�����Դ�ҵĸм�֮�飩��V0.8.0 �汾��Ҫ��֧���˵�¼�������ռ䡢Metrics��أ��Խ�Prometheus����ͨ��Nacos-Sync ���֧�ִӴ�ͳ��ע������ƽ������Nacos��������Ǩ�Ƶ����ԣ��Ը��ȶ��͸��߿��õ���̬���û�������������֧�Ŵ�ҵ�΢����ƽ̨��

### Nacos ��¼
Nacos����̨֧�ֵ�¼���ǳ����ԣ��Ա����ȫ��������ʹ�á�<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/9687/1548047848570-c92c232f-13eb-41e3-a8af-0660e3a58912.png#align=left&display=inline&height=894&linkTarget=_blank&name=image.png&originHeight=1430&originWidth=2876&size=195009&width=1797)


### �����ռ�
Nacos��0.5.0�汾֧�������ռ����������÷�����֧���������ռ䣬������ģ���������0.8.0�汾֧���˶������ռ䣬ʹ�÷����ֵ������ռ����ʵ�ַ������ݵ��߼����롣ʹ�÷�����ģ��Ķ������ռ�������ģ�������ͬ����Nacos����̨�ϲ鿴��Ҫʹ�õ������ռ�ID���ڿͻ�����ʱ����������ռ�ID��

```java
Properties properties = new Properties();

properties.put(PropertyKeyConst.NAMESPACE, "74a3dbb9-36cb-43f5-8d31-006acfd61caa");

properties.put(PropertyKeyConst.SERVER_ADDR, "127.0.0.1:8848");

NamingService naming = NamingFactory.createNamingService(properties);
```

����ͨ�����NamingServiceʵ����д�ľͶ��������ռ�74a3dbb9-36cb-43f5-8d31-006acfd61caa�µ������ˡ���Ȼ��Ҳ���Բ�ָ�������ռ�ID����������Ĭ�Ϸ��䵽public�����ռ䡣�����������Ե�Nacos����̨�ϲ�ѯ������Ϣ��<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/9687/1548312345294-d4bd95df-7e6d-4a36-8827-6a7ac0a00985.png#align=left&display=inline&height=553&linkTarget=_blank&name=image.png&originHeight=830&originWidth=1904&size=131287&width=1269)

### Metrics���
ͨ��Metrics��Ϣ��¶���Խ�Prometheus��ǿNacosʵʱ��أ��Ա����û��Բ�Ʒ���п�������

Nacos ͨ��micrometerͳ��������ʱ�ĺ���ָ�꣺
* ϵͳָ�����cpu load jvm��
* ҵ��ָ��������������������������ӣ�QPS��RT��
* �쳣ָ���¼��Nacos���е��ڲ��쳣micrometer�ṩ��ת������ת���ɶ���metrics��ʽ��NacosĿǰ֧�ֳ��õ�prometheus��elastic search��influxdb���������Ը��ݾ���������е�����

<br /><br />grafana�߱�ǿ��ĵ����ݿ��ӻ��������ܽ��ɼ�������չʾ������֧�ֶ�������Դ��ͬʱ�ɶ���Ҫָ�����ø澯�������ݴﵽ��ֵʱ����֪ͨ��ظ����ˡ�<br />Nacos�����ṩ�˽��prometheus��grafanaʵ��metrics���<br /><br /><br />![](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/53357/1548122164953-6011a9ee-a521-447c-a871-7ebcf10c2ce4.png#align=left&display=inline&height=417&linkTarget=_blank&originHeight=1584&originWidth=2832&size=0&width=746)

�����������Բο�����[����ĵ�](https://nacos.io/zh-cn/docs/monitor-guide.html)��
### 
### Nacos-Sync ֧�ַ���ƽ��Ǩ��

�ṩNacos-Syncͬ������֧���û����������ݵ�ƽ��Ǩ��Ǩ�ƣ�֧���û�������ע������ƽ��Ǩ�Ƶ�Nacos������ͬʱ֧�ֶ��Region����Nacos����ͬ����ĿǰNacos-Sync֧�ֵ�Դע��������Ҫ����ZooKeeper,Eureka�ȡ�

#### ʹ�ó���
* ˫��ͬ������,֧��Dubbo+Zookeeper����ƽ��Ǩ�Ƶ�Dubbo+Naocs,����Nacos�������ʵķ���

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/4232/1548136490076-13655b30-b0e4-4363-95dc-72b79a080fc0.png#align=left&display=inline&height=246&linkTarget=_blank&name=image.png&originHeight=838&originWidth=1728&size=171454&width=508)

* ������绥ͨ��Region֮�������,����Region֮��ķ����������

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/4232/1548136895122-ba2be529-d959-4c9d-9fa4-74059bce1d18.png#align=left&display=inline&height=399&linkTarget=_blank&name=image.png&originHeight=798&originWidth=1136&size=64731&width=568)

#### ֧�ֵķ�Χ
Nacos-Sync֧���û���չ��ͬע�����ķ���ͬ����Ŀǰ��֧�ֵ�ͬ����������:
* Nacos����ͬ����Nacos
* Zookeeper����ͬ����Nacos
* Nacos����ͬ����Zookeeper
* Eureka����ͬ����Nacos
* Consul����ͬ����Nacos

#### ����ͬ������
Nacos-Sync�ṩ�˿���̨����������ͬ���ķ�������:
* ͬ���������ҳ��

![](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/4232/1548129423366-e1a37af4-3eb6-48f0-af76-84ec1f310ee2.png#align=left&display=inline&height=277&linkTarget=_blank&originHeight=1064&originWidth=2866&width=746)
* ע�����Ĺ���ҳ��
## ![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/4232/1548129453620-f480a696-931b-4db4-b4c7-298ae7da029e.png#align=left&display=inline&height=562&linkTarget=_blank&name=image.png&originHeight=1124&originWidth=2876&size=190668&width=1438)

������Ŀ��Ϣ��ο�[Nacos-Sync��Ʒҳ](https://github.com/nacos-group/nacos-sync)

## ���չ�� Nacos ����

> DISS is cheap, show me your hand
���²۸���Ҫ���Ǵ���֣���������һ��չNacos


* ��Ϊ�û���ע�ͼ��� Nacos ����

Nacos �����������չ����ֹ������Ϊֹ��Nacos �̶̼������Ѿ��� 9 ��΢��Ⱥ������ 7 ������Ա��1��QQȺ��1������Ⱥ����ע Nacos �����������Ѿ���5000�ˣ��� Nacos Ⱥ��� �����������ѡ� �д輼�����������飬��Ƹ���ѣ��������...�����ֺ���

Ҫ���� Nacos ΢�������������ͨ��ɨ�����**�����硱**�����硱** �������� ��Nacos����΢�Ž���Ⱥ��


![](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/9687/1548047927520-89c34af8-899a-41b6-887c-9319461db519.png#align=left&display=inline&height=424&linkTarget=_blank&originHeight=1124&originWidth=1984&size=0&width=748)

* ��Ϊ���빱���߼��� Nacos ����

��Nacos�û���չ���ɹ�����˳����£���Nacos�����Ŷ�Ҳȷʵ������׳�󣬴ӿ�ʼ��ֻ��4������contributor��չ��Ŀǰ��34������0.8.0 �汾�Ŀ����У�����ͬѧ�����˺ܴ���������ڴ��ر��л����ͬѧ��Ƶ�¼UI�������ͬѧ���׵�¼���룬������ͬѧ���������ռ���룬����ͬѧ����nacos-sync���룬�ͬѧ�������ù�����룬����ͬѧ��֤����ؼ��汾�Ĳ������������ź����и���ͬѧ���뵽Nacos�����Ĺ����С�

������Ҳ���ڼƻ��ں��ʵ�ʱ���ϣ�����Nacos���� [nacos.io](http://nacos.io/) ������Ŷӽ���ҳ���������ʽ�������ڣ���ӭ��Ҽ���Nacos������������������Apache�Ļ�˵��**���������ڴ��롱!**


![](https://cdn.nlark.com/lark/0/2018/png/15914/1542704700864-a9d54856-9bf6-4176-b449-c13fa02c5800.png#align=left&display=inline&height=387&linkTarget=_blank&originHeight=888&originWidth=1716&width=748)

## [](https://yuque.alibaba-inc.com/nacos/opensource/dawygn#6gw6hq)����ʱ�� - "ʲô��Nacos��"
> ����֪��ʲô��Nacos? û��ϵ����github��starһ�¸�����Գ�ֵܴ���к���!!


[Nacos](https://github.com/alibaba/nacos) �ǰ���Ͱ���7�·��¿�Դ����Ŀ��Nacos����ҪԸ��������ͨ���ṩ���õ� `��̬������`��`�������ù���`��`�����������` �Ļ�����ʩ�������û�����ԭ��ʱ�����õĹ����������������Լ���΢����ƽ̨��


![](https://cdn.nlark.com/lark/0/2018/png/15914/1532436633419-08a42307-7fb7-4d51-9062-fecc3868613b.png#align=left&display=inline&height=355&linkTarget=_blank&originHeight=1014&originWidth=2138&width=748)

github��Ŀ��ַ�� [����](https://github.com/alibaba/nacos)

## [](https://yuque.alibaba-inc.com/nacos/opensource/dawygn#kn9iog)������ Nacos ��صĿ�Դ��Ŀ��Ϣ

* [Nacos](https://github.com/alibaba/nacos)
* [Dubbo Registry Nacos](https://github.com/dubbo/dubbo-registry-nacos)
* [Nacos DNS-F](https://github.com/nacos-group/nacos-coredns-plugin)
* [Nacos Docker](https://github.com/nacos-group/nacos-docker)
* [Nacos Spring Project](https://github.com/nacos-group/nacos-spring-project)
* [Nacos Spring Boot](https://github.com/nacos-group/nacos-spring-boot-project)
* [Spring Cloud Alibaba](https://github.com/spring-cloud-incubator/spring-cloud-alibaba)
* [Dubbo](http://dubbo.io/)
* [Sentinel](https://github.com/alibaba/Sentinel)
* [Spring Cloud](https://projects.spring.io/spring-cloud/)
* [Nepxion Discovery](https://github.com/Nepxion/Discovery)
* [Spring Cloud Gateway Nacos](https://github.com/SpringCloud/spring-cloud-gateway-nacos)

