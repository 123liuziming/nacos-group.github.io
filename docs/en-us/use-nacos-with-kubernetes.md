# Kubernetes Nacos


����Ŀ����һ���ɹ�����Nacos Docker Image,ּ������StatefulSets��[Kubernetes](https://kubernetes.io/)�ϲ���[Nacos](https://nacos.io)

[English Document](https://github.com/nacos-group/nacos-k8s/blob/master/README.md)

# ���ٿ�ʼ

* **Clone ��Ŀ**


```shell
git clone https://github.com/nacos-group/nacos-k8s.git
```



* **������**

> �����ʹ�ü򵥷�ʽ��������,��ע������û��ʹ�ó־û����,���ܴ������ݶ�ʧ����:

```shell
cd nacos-k8s
chmod +x quick-startup.sh
./quick-startup.sh
```



* **����**

  * **����ע��**

  ```bash
  curl -X PUT 'http://cluster-ip:8848/nacos/v1/ns/instance?serviceName=nacos.naming.serviceName&ip=20.18.7.10&port=8080'
  ```



  * **������**

  ```bash
  curl -X GET 'http://cluster-ip:8848/nacos/v1/ns/instances?serviceName=nacos.naming.serviceName'
  ```



  * **��������**

  ```bash
  curl -X POST "http://cluster-ip:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=helloWorld"
  ```



  * **��ȡ����**

  ```bash
  curl -X GET "http://cluster-ip:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"
  ```



# �߼�ʹ��

> �ڸ߼�ʹ����,Nacos��K8Sӵ���Զ��������ݺ����ݳ־�����,��ע�������Ҫʹ���ⲿ�ֹ�����ʹ��PVC�־þ�,Nacos���Զ�����������Ҫ�����־þ�,�Լ����ݳ־û�Ҳ��һ��,������ʹ�õ���NFS��ʹ��PVC.
>



## ���� NFS

* ������ɫ 

```shell
kubectl create -f deploy/nfs/rbac.yaml
```

> �����K8S�����ռ䲻��**default**,���ڲ���RBAC֮ǰִ�����½ű�:


```shell
# Set the subject of the RBAC objects to the current namespace where the provisioner is being deployed
$ NS=$(kubectl config get-contexts|grep -e "^\*" |awk '{print $5}')
$ NAMESPACE=${NS:-default}
$ sed -i'' "s/namespace:.*/namespace: $NAMESPACE/g" ./deploy/nfs/rbac.yaml

```



* ���� `ServiceAccount` �Ͳ��� `NFS-Client Provisioner`

```shell
kubectl create -f deploy/nfs/deployment.yaml
```



* ���� NFS StorageClass

```shell
kubectl create -f deploy/nfs/class.yaml
```



* ��֤NFS����ɹ�

```shell
kubectl get pod -l app=nfs-client-provisioner
```



## �������ݿ�


* ��������

```shell

cd nacos-k8s

kubectl create -f deploy/mysql/mysql-master-nfs.yaml
```



* ����ӿ�

```shell

cd nacos-k8s 

kubectl create -f deploy/mysql/mysql-slave-nfs.yaml
```



* ��֤���ݿ��Ƿ���������

```shell
# master
kubectl get pod 
NAME                         READY   STATUS    RESTARTS   AGE
mysql-master-gf2vd                        1/1     Running   0          111m

# slave
kubectl get pod 
mysql-slave-kf9cb                         1/1     Running   0          110m
```



## ����Nacos



* �޸�  **depoly/nacos/nacos-pvc-nfs.yaml**

```yaml
data:
  mysql.master.db.name: "��������"
  mysql.master.port: "����˿�"
  mysql.slave.port: "�ӿ�˿�"
  mysql.master.user: "�����û���"
  mysql.master.password: "��������"
```



* ���� Nacos

``` shell
kubectl create -f nacos-k8s/deploy/nacos/nacos-pvc-nfs.yaml
```



* ��֤Nacos�ڵ������ɹ�

```shell
kubectl get pod -l app=nacos


NAME      READY   STATUS    RESTARTS   AGE
nacos-0   1/1     Running   0          19h
nacos-1   1/1     Running   0          19h
nacos-2   1/1     Running   0          19h
```





## ���ݲ���

* ������ǰ,ʹ�� [`kubectl exec`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands/#exec)��ȡ��pod�е�Nacos��Ⱥ�����ļ���Ϣ

```powershell
for i in 0 1; do echo nacos-$i; kubectl exec nacos-$i cat conf/cluster.conf; done
```

StatefulSet��������������������Ϊÿ��Pod�ṩΨһ���������� ����������<statefulset name>  -  <ordinal index>����ʽ�� ��Ϊnacos StatefulSet�ĸ����ֶ�����Ϊ2�����Ե�ǰ��Ⱥ�ļ���ֻ������Nacos�ڵ��ַ



![k8s](/images/k8s.gif)



* ʹ��kubectl scale ��Nacos��̬����

```bash
kubectl scale sts nacos --replicas=3
```

![scale](/images/scale.gif)



* �����ݺ�,ʹ�� [`kubectl exec`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands/#exec)��ȡ��pod�е�Nacos��Ⱥ�����ļ���Ϣ

```bash
for i in 0 1 2; do echo nacos-$i; kubectl exec nacos-$i cat conf/cluster.conf; done
```

![get_cluster_after](/images/get_cluster_after.gif)



* ʹ�� [`kubectl exec`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands/#exec)ִ��Nacos API ��ÿ̨�ڵ��ϻ�ȡ��ǰ**Leader**�Ƿ�һ��

```bash
for i in 0 1 2; do echo nacos-$i; kubectl exec nacos-$i curl GET "http://localhost:8848/nacos/v1/ns/raft/state"; done
```

����������Է����½ڵ��Ѿ���������Nacos��Ⱥ����

# ���Ӳ��𻷾�

- ��������

| ����IP      | ������     | ����                                                         |
| ----------- | ---------- | ------------------------------------------------------------ |
| 172.17.79.3 | k8s-master | CentOS Linux release 7.4.1708 (Core) Single-core processor Mem 4G Cloud disk 40G |
| 172.17.79.4 | node01     | CentOS Linux release 7.4.1708 (Core) Single-core processor Mem 4G Cloud disk 40G |
| 172.17.79.5 | node02     | CentOS Linux release 7.4.1708 (Core) Single-core processor Mem 4G Cloud disk 40G |

- Kubernetes �汾��**1.12.2** ����������һ��ֻʹ������̨����,��ô�ǵÿ���master�ڵ�Ĳ����ܣ�
- NFS �汾��**4.1** ��k8s-master���а�װServer��,����ָ������Ŀ¼,����Ŀָ����**/data/nfs-share**
- Git



# ����

* ����Ҫʹ�ó־þ�,�����������ݶ�ʧ�����





# ��ĿĿ¼

| Ŀ¼ | ����                                |
| ------ | ----------------------------------- |
| plugin | ����Nacos��Ⱥ���ж�̬���ݵĲ��Docker����Դ�� |
| deploy | K8s �����ļ�              |



# ��������

* nacos-pvc-nfs.yaml or nacos-quick-start.yaml 

| ����                  | ��Ҫ | ����                                    |
| --------------------- | -------- | --------------------------------------- |
| mysql.master.db.name  | Y       | ��������                      |
| mysql.master.port     | N       | ����˿�                        |
| mysql.slave.port      | N       | �ӿ�˿�                       |
| mysql.master.user     | Y       | �����û���                     |
| mysql.master.password | Y       | ��������                     |
| NACOS_REPLICAS        | N      | ȷ��ִ��Nacos�����ڵ�����,��������ö�̬���ݲ��,�ͱ�������������ԣ�����ʹ�����ݲ���󲻻���Ч |
| NACOS_SERVER_PORT     | N       | Nacos �˿�             |
| PREFER_HOST_MODE      | Y       | ����Nacos��Ⱥ���������� |



* **nfs** deployment.yaml 

| ����       | ��Ҫ | ����                     |
| ---------- | -------- | ------------------------ |
| NFS_SERVER | Y       | NFS ����˵�ַ         |
| NFS_PATH   | Y       | NFS ����Ŀ¼ |
| server     | Y       | NFS ����˵�ַ  |
| path       | Y       | NFS ����Ŀ¼ |



* mysql 

| ����                     | ��Ҫ | ����                                                      |
| -------------------------- | -------- | ----------------------------------------------------------- |
| MYSQL_ROOT_PASSWORD        | N       | ROOT ����                                                    |
| MYSQL_DATABASE             | Y       | ���ݿ�����                                   |
| MYSQL_USER                 | Y       | ���ݿ��û���                                  |
| MYSQL_PASSWORD             | Y       | ���ݿ�����                              |
| MYSQL_REPLICATION_USER     | Y       | ���ݿ⸴���û�            |
| MYSQL_REPLICATION_PASSWORD | Y       | ���ݿ⸴���û�����      |
| Nfs:server                 | N      | NFS ����˵�ַ�����ʹ�ñ��ز�����Ҫ���� |
| Nfs:path                   | N     | NFS ����Ŀ¼�����ʹ�ñ��ز�����Ҫ���� |





