# 27 | 聪明的微创新：Operator工作原理解读

使用Etcd Operator的方法非常简单，只要两步：

1. 将这个Operator的代码Clone到本地
```shell
git clone https://github.com/coreos/etcd-operator
```

2. 将这个Etcd Operator部署在Kubernetes集群里
```shell
./example/rbac/create_role.sh
```

以上主要创建一个`etcd-operator`的角色(Role)，并与`default`的`ServiceAccount`做绑定。

etcd-operator定义了如下的权限：
```shell
1. 对Pod、Service、PVC、Deployment、Secret等API对象，有所有权限。
2. 对CRD对象，有所有权限。
3. 对属于etcd.database.coreos.com这个API Group的CR(Custom Resource)对象，有所有权限。
```

**而Etcd Operator本身，其实就是一个Deployment。**

Etcd Operator本身，其实就是一个Deployment，它的yaml文件在[这里](./notefile/etcd-operator-deployment.yaml)(这个文件相对于github项目
中的进行了一定的修改，如selector等内容)。执行：
```shell
kubectl apply -f etcd-operator-deployment.yaml
```
当Etcd Operator的Pod进入了Running状态，就会发现有一个CRD被自动创建了出来。
```shell
kubectl get crd | grep etcd
```
通过对该CRD进行查看：
```shell
kubectl describe crd etcdclusters.etcd.database.coreos.com
```

通过上述两步操作，成功在Kubernetes中添加了一个名叫EtcdCluster的自定义资源类型。
**而Etcd Operator本身，就是这个自定义资源类型的自定义控制器。**

可以通过执行example-etcd-cluster.yaml文件来创建etcdclusters.etcd.database.coreos.com API对象。
```shell
kubectl apply -f example/example-etcd-cluster.yaml
```

