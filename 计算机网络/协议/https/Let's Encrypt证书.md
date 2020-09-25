## 生成RSA私钥

首先创建一个目录，例如 `ssl`:

账户私钥：account.key

```sh
openssl genrsa 4096 > account.key
```

域名私钥：domain.key

```sh
openssl genrsa 4096 > domain.key
```

## 生成CSR（Certificate Signing Request，证书签名请求）

有了私钥文件，就可以生成 CSR 文件

```sh
openssl req -new -sha256 -key domain.key -subj "/" -reqexts SAN -config <(cat /etc/ssl/openssl.cnf <(printf "[SAN]\nsubjectAltName=DNS:yoursite.com,DNS:www.yoursite.com")) > domain.csr
```

## 验证服务

Let's Encrypt 是在你的服务器上生成一个随机验证文件，再通过创建 CSR 时指定的域名访问，如果可以访问则表明你对这个域名有控制权。

创建用于存放验证文件的目录：

```sh
mkdir ~/www/challenges/
```

配置一个 HTTP 服务，以 Nginx 为例：

```sh
server {
    server_name www.yoursite.com yoursite.com;

    location ^~ /.well-known/acme-challenge/ {
        alias /home/zhujue/www/challenges/;
        try_files $uri =404;
    }

    location / {
        rewrite ^/(.*)$ https://yoursite.com/$1 permanent;
    }
}
```

以上配置优先查找 `~/www/challenges/` 目录下的文件，如果找不到就重定向到 HTTPS 地址。这个验证服务以后更新证书还要用到，建议一直保留。

### 获取网站证书

把 acme-tiny 脚本保存到之前的 `ssl` 目录：

```sh
git clone https://github.com/diafygi/acme-tiny.git
```

指定账户私钥、CSR 以及验证目录，执行脚本：

```sh
python acme_tiny.py --account-key ../account.key --csr ../domain.csr --acme-dir /home/zhujue/www/challenges/ > ../signed.crt
```

如果一切正常，当前目录下就会生成一个 `signed.crt`，这就是申请好的证书文件。

## 下载 Let's Encrypt 的中间证书

配置 HTTPS 证书时既不要漏掉中间证书，也不要包含根证书。在 Nginx 配置中，需要把中间证书和网站证书合在一起：

```sh
wget -O - https://letsencrypt.org/certs/lets-encrypt-x3-cross-signed.pem > intermediate.pem
cat signed.crt intermediate.pem > chained.pem
```

最终，修改 Nginx 中有关证书的配置并 reload 服务即可：

```sh
ssl_certificate     ~/www/ssl/chained.pem;
ssl_certificate_key ~/www/ssl/domain.key;
```

## 配置自动更新

Let's Encrypt 签发的证书只有 90 天有效期，推荐使用脚本定期更新。例如我就创建了一个 `renew_cert.sh` :

```sh
#!/bin/bash

cd /home/xxx/www/ssl/
python acme_tiny.py --account-key account.key --csr domain.csr --acme-dir /home/xxx/www/challenges/ > signed.crt || exit
wget -O - https://letsencrypt.org/certs/lets-encrypt-x3-cross-signed.pem > intermediate.pem
cat signed.crt intermediate.pem > chained.pem
service nginx reload
```



参考资料：

https://imququ.com/post/letsencrypt-certificate.html