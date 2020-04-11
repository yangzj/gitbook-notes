一个容器实际，实际上由Linux Namespace、Linux Cgroups与rootfs三种技术构建出来的隔离环境。

一个运行中的容器，可以被”一分为二“来看待：

静态视图：一组联合挂载在/var/lib/docker/aufs/mnt上的rootfs，这一部分我们成为“容器镜像”

动态视图：一个由Namespace+Cgroup构成的隔离环境，这一部分我们称为“容器运行时”