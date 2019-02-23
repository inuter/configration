# 在Linux操作系统中配置JDK

1. 查看当前操作系统是否安装了openjdk
```sh
sudo dpkg --list | grep -i jdk
```

2. 删除openjdk
```sh
sudo apt-get purge openjdk*
```

3. 删除其它的包
```sh
sudo apt-get purge icedtea-* openjdk-*
cd /usr/lib/jvm （如果没有jvm这个目录，就不用管这步了）
sudo rm -rf jdk<version>
```

4. 确认openjdk已经被完全删除
```sh
sudo dpkg --list | grep -i jdk
```

5. 下载JDK。有 `rpm` 和 `.tar.gz`版本

6. 解压 `.tar.gz` 压缩包
```sh
tar -zxvf jdk-xxx
```

7. 在 `/opt` 新建一个文件夹
```sh
sudo mkdir -p /opt/java
```

8. 移动解压文件至 `/opt/java`
```sh
sudo mv jdk1.xxx /opt/java
```

9. 设置环境变量
```sh
sudo touch /etc/profile.d/jdk.sh

vim /etc/profile.d/jdk.sh

JAVA_HOME=/opt/java/jdk1.8.0_202/
PATH=$JAVA_HOME/bin:$PATH
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

export JAVA_HOME
export PATH
export CLASSPATH
```

10. 刷新环境变量
```sh
source /etc/profile
```

11. 验证是否安装成功
```sh
java -version
```
