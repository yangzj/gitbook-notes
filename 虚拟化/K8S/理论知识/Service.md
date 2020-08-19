# 概念

Service 是 Kubernetes 项目中用来将 一组 Pod 暴露给外界访问的一种机制。比如，一个 Deployment 有 3 个 Pod，那么我就可以 定义一个 Service。然后，用户只要能访问到这个 Service，它就能访问到某个具体的 Pod。

# 如何被访问

1. 以 Service 的 VIP（Virtual IP，即：虚拟 IP）方式。比如：当我访问 10.0.23.1 这个 Service 的 IP 地址时，10.0.23.1 其实就是一个 VIP，它会把请求转发到该 Service 所代理 的某一个 Pod 上。

2. 是以 Service 的 DNS 方式。比如：这时候，只要我访问“my-svc.mynamespace.svc.cluster.local”这条 DNS 记录，就可以访问到名叫 my-svc 的 Service 所代理 的某一个 Pod。具体还可以分为两种处理方法：

   - Normal Service。这种情况下，你访问“my-svc.mynamespace.svc.cluster.local”解析到的，正是 my-svc 这个 Service 的 VIP，后面的流程就跟 VIP 方式一致了。

   - Headless Service。这种情况下，你访问“my-svc.mynamespace.svc.cluster.local”解析到的，直接就是 my-svc 代理的某一个 Pod 的 IP 地址。可以看到，这里的区别在于，Headless Service 不需要分配一个 VIP，而是可以直接以 DNS 记录的方式解析出被代理Pod 的 IP 地址。

     > 当你按照这样的方式创建了一个 Headless Service 之后，它所代理的所有 Pod 的 IP 地址，都 会被绑定一个这样格式的 DNS 记录，如下所示：
     >
     > `<pod-name>.<svc-name>.<namespace>.svc.cluster.local`
     >
     > 这个 DNS 记录，正是 Kubernetes 项目为 Pod 分配的唯一的“可解析身份”（Resolvable Identity）。
     >
     > 有了这个“可解析身份”，只要你知道了一个 Pod 的名字，以及它对应的 Service 的名字，你 就可以非常确定地通过这条 DNS 记录访问到 Pod 的 IP 地址。

