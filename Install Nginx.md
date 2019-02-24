# nginx

> 官方教程：[查看](https://docs.nginx.com/nginx/admin-guide/)

1. Installing NGINX Dependencies    
   Prior to compiling NGINX Open Source from source, we need to install libraries for its dependencies: 

   * `PCRE` – Supports regular expressions. Required by the NGINX Core and Rewrite modules.
   * `zlib` – Supports header compression. Required by the NGINX Gzip module.
   * `OpenSSL` – Supports the HTTPS protocol. Required by the NGINX SSL module and others.

2. Downloading the Sources
```sh
$ wget https://nginx.org/download/nginx-x.x.x.tar.gz
$ tar zxf nginx-x.x.x.tar.gz
```

3. Configuring, Building and Installing

```sh
$ ./configure
$ make
$ make install
```
