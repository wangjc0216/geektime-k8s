# 26 | 基于角色的权限控制：RBAC

RBAC,Role-based access control,基于角色控制权限。

Kubernetes中所有API对象，都保存在etcd中，对这些API对象的操作，都是通过访问kube-apiserver来实现的，这里一个很重要的原因就是你需要apiserver
帮您做授权工作。

在Kubernetes中，负责完成授权(Authorization)的机制，就是RBAC，基于角色的访问控制。

在RBAC中，需要明确三个概念：
> 1. Role:角色，它其实是一种规则，定义了一组Kubernetes API对象的访问权限。
> 2. Subject: 被调用者，可以是人，也可以是机器，如Kubernete ServiceAccount对象。
> 3. Rolebinding: 被调用者与角色的绑定关系。

Subject 可以是多种，如User、ServiceAccount(内置用户)、Group(用户组).

ServiceAccount如下：
```shell
system:serviceaccount::
```
Group如下：
```shell
system:serviceaccounts:
```

如是系统内置角色，它的名字是system:<名字> 组成的。
```shell
kubectl describe clusterrole system:kube-scheduler
```

除了系统内置角色(带system:的)，还有四个定义好的ClusterRole来进行选择：
```shell
cluster-admin；admin；edit；view。
```

