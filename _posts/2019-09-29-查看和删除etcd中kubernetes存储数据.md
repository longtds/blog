###### 预先通过docker exec 进入etcd容器
#### 查看etcd数据结构:
ETCDCTL_API=3 etcdctl get /registry/deployments/default --prefix --keys-only

#### Kubernetes中强制删除Pod、namespace
解决方法
可使用kubectl中的强制删除命令
######  删除POD
kubectl delete pod PODNAME --force --grace-period=0

######  删除NAMESPACE
kubectl delete namespace NAMESPACENAME --force --grace-period=0
若以上方法无法删除，可使用第二种方法，直接从ETCD中删除源数据
#### 删除default namespace下的pod名为pod-to-be-deleted-0
ETCDCTL_API=3 etcdctl del /registry/pods/default/pod-to-be-deleted-0

####  删除需要删除的NAMESPACE
etcdctl del /registry/namespaces/NAMESPACENAME