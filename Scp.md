# scp

```text
NAME
     scp — secure copy (remote file copy program)

SYNOPSIS
     scp [-346BCpqrTv] [-c cipher] [-F ssh_config] [-i identity_file]
         [-l limit] [-o ssh_option] [-P port] [-S program]
         [[user@]host1:]file1 ... [[user@]host2:]file2

DESCRIPTION
     scp copies files between hosts on a network.  It uses ssh(1) for data
     transfer, and uses the same authentication and provides the same security
     as ssh(1).  scp will ask for passwords or passphrases if they are needed
     for authentication.

     File names may contain a user and host specification to indicate that the
     file is to be copied to/from that host.  Local file names can be made
     explicit using absolute or relative pathnames to avoid scp treating file
     names containing ‘:’ as host specifiers.  Copies between two remote hosts
     are also permitted.
```

1. 上传本地文件到服务器
```sh
scp /local_dir/filename username@servername:/path/
```

2. 从服务器下载文件
```sh
scp username@servername:/path/filename /local_dir
```

3. 从服务器下载整个目录
```sh
scp -r username@servername:/remote_dir  /local_dir（本地目录）
```

4. 上传整个目录到服务器
```sh
scp -r /local_dir username@servername:/remote_dir
```
> 本地路径可使用绝对路径也可以使用相对路径