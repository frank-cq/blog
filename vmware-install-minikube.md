近两年云原生大火，k8s 大火，docker、敏捷、devops 纷至杳来。之前做预研项目一直是在公司小伙伴提供的 kubernets 集群上，为了方便随时实验，还是需要在个人开发环境装一个小型的 minikube。

有一种认识在脑中逐渐形成（也许是被万恶的 google 洗脑也说不定）：k8s 可能会变成像操作系统一样普遍的事物，但位置是在操作系统之上，整合服务器的物理资源（这又是分层思想的一个应用，分层思想万岁）。对于开发来说，熟悉 linux 已经变成一个默认的技能，未来还会增加熟悉 k8s，所以务必像熟悉 linux 一样熟悉 k8s，程序员作为手艺工种，基本功非常重要。


环境
> 宿主机：Win10
> 虚拟机：Ubuntu18.04-x64-desktop
> 虚拟机内存：6G
> 虚拟机存储：40G
> Vmware Workstation 版本：15.5.0

1、安装常用工具
```bash
# 安装常用工具及 docker，非常喜欢的 fish
# 人生苦短，记得换源
sudo apt install -y fish vim openssh-server curl docker.io
```

2、安装 minikube，[传送](https://minikube.sigs.k8s.io/docs/start/linux/)
```bash
# 看到带 google 的地址总是比较惊恐，毕竟人生苦短，不过这个可以正常访问
sudo curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

3、启动 minikube，启动时会去拉取镜像，默认是 gcr.io，所以这里最重要的就是换镜像仓库，毕竟现实会教育你什么叫人生苦短，[传送](https://github.com/kubernetes/minikube/issues/4224)
```bash
# sudo minikube start --vm-driver=none --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers --alsologtostderr --v=7
minikube start --vm-driver=none --image-mirror-country=cn --alsologtostderr --v=7
```

4、安装 kubectl，[传送](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
```bash
# 有 google 别怕，大胆地输入执行
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl

chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

5、最后验证
```bash
kubectl cluster-info
```

现在可以去写 yaml 文件疯狂创建 ns、svc、deployment、po、cm、pvc ...

友情提示：设置好 alias，毕竟人生苦短 && 程序员憎恶重复

