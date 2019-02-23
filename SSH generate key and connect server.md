# SSH

1. 生成密钥
```sh
ssh-keygen -t rsa -C "备注"
```

```sh
NAME
     ssh-keygen — authentication key generation, management and conversion

SYNOPSIS
     ssh-keygen [-b bits] [-t dsa | ecdsa | ed25519 | rsa]
                [-N new_passphrase] [-C comment] [-f output_keyfile]
```

**private key: id_rsa**    
**public key: id_rsa.pub**    
本地保留私钥，服务端配置公钥

2. Github SSH 配置     
  参考：[Connecting to GitHub with SSH](https://help.github.com/en/articles/connecting-to-github-with-ssh)

```text
Testing your SSH connection

$ ssh -T git@github.com
```

3. SSH 连接
```sh
$ ssh username@192.168.0.1 [-p port] [-i private key]
```
