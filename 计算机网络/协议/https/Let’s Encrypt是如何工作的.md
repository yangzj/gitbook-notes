Let's Encrypt是一个CA，官网介绍了其详细工作原理，我按照自己的理解复述一下：

通过为https://example.com/设置证书管理代理这个过程（该代理需支持Let's Encrypt），我们可以了解Let's Encrypt是如何工作的。

这个过程分两步：首先，代理向CA证明web服务器拥有域控制权（域认证）；其后，代理可以为该域请求，更新，撤销证书（证书发放与撤销）。

域认证

Let’s Encrypt（后面简写CA）通过公钥来标识服务器管理员。代理在第一次与Let’s Encrypt通信的时候，会产生一个秘钥对（公钥与私钥），并且向CA证明服务器拥有一个或多个域，这类似于传统的CA认证过程：创建一个账号，并为该账号加入域。

为了开始这个流程，代理会询问CA为了证明自己拥有example.com域需要做些什么。CA会查看代理请求的域名并发出一组或多组challenges(可以理解是CA给代理下发的任务，后续CA通过验证该任务的完成情况来证明代理拥有域控制权)。代理有多重不同的方式来证明拥有域的控制权。例如：CA可以给代理下面两种选择：

1）配置一个从属于域example.com的DNS记录   (参见Certbot, Challenge Type:dns-01)

2) 在https://example.com/上的一个众所周知的URI上配置一个http资源 (参见Certbot, Challenge Type:http-01)

伴随着challenges，CA还会提供一个随机数(这个随机数只会被使用一次)，代理必须用它的私钥为这个随机数签名，用来证明代理拥有这个秘钥对的控制权。（下图,put ed98 at https://example.com/8303代表一个challenge，意思是让代理将ed98写入https://example.com/8303指向的文件资源。）



![Requesting challenges to validate example.com](https://letsencrypt.org/images/howitworks_challenge.png)



代理软件完成了一组CA提供的challenges。在这里我们假设代理完成是CA提供的第二种选择（Challenge Type:http-01）：在http://example.co/站点的一个指定的路径下（8303）创建一个文件（写入ed98）。同时代理用自己的私钥为CA提供的随机数签名。一旦代理完成这些步骤，就会通知CA它已经准备等待验证完成。

然后，CA的工作是核实那些challenges是否被满足。CA会验证随机数的签名（CA收到代理发送过来的签名以及公钥A，用公钥A对签名解密，得到数字摘要，和随机数生成的摘要做对比，一致则证明这个签名是代理的签名。），并且会尝试从web服务器下载文件(https://example.com/8303)，并确认文件内容是所期望的内容（ed98）。

![Requesting authorization to act for example.com](https://letsencrypt.org/images/howitworks_authorization.png)

如果随机数的签名是合法的，并且challenges检查合格。被公钥标识的代理被授权为域example.com管理证书。我们称代理使用的密钥对 为域example.com的已授权密钥对。

证书发放与撤销

一旦代理有了已授权秘钥对，请求，更新，撤销证书就很简单了，只需要发送证书管理消息，并用授权秘钥对他们签名就可以了。

为了获取域证书，代理构建一个PKCS#10证书签名请求(CSR)给CA,请求CA使用指定的公钥来发放域example.com证书。通常，CSR中包含了由一个在CSR中的公钥关联的私钥加密的签名。代理会用域example.com的已授权秘钥为整个CSR签名，以便让CA知道自己是被授权的。

当CA接收到请求，会验证两个签名。如果两个签名都是正常的，CA会为域example.com发放证书以及CSR中的公钥，一并返回给代理。

![Requesting a certificate for example.com](https://letsencrypt.org/images/howitworks_certificate.png)

 

 

注：该篇翻译了代理与LE交互的部分过程。LE使用ACME协议来完成域认证和证书发放，客户端代理必须使用ACME协议与LE通信。

实现ACME协议的客户端有很多，LE官网推荐使用Certbot，具体使用可参见Certbot官网。

challenges可参见certbot说明，一般有http-01,dns-01,tls-sni-01这三种。





https://letsencrypt.org/zh-cn/how-it-works/

https://www.cnblogs.com/gao88/p/10593306.html