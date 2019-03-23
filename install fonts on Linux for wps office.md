# install fonts on Linux for wps office
> **Author: liming zhong**    
> **Date: Mon Mar 18 12:38:10 CST 2019**

1. install wps with deb package

2. download fonts package [download](https://pan.baidu.com/s/1eS6xIzo)

3. create a directory on /usr/share/fonts/truetype and named "wps-office"

4. unzip the fonts package that you download to /usr/share/fonts/truetype/wps-office

```sh
sudo unzip package -d /usr/share/fonts/truetype/wps-office
```

5. refresh cache use the command below
```sh
sudo fc-cache
```