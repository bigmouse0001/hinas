**一、电脑浏览器输入机顶盒ip地址**

账号：root
密码：ecoo1234 (输密码不显示，输入完按确认即可)

开通frp权限，kaitong-frp

**二、安装docker**

#安装docker
`apt update && apt install docker.io`
看终端提示，输入y，回车确认

**三、安装docker面板**

#安装docker面板
`install-portainer.sh`

#浏览器输入 http://你的路由器ip:9000
形如：192.168.1.8:9000，进入docker面板设置账号密码

**四、安装book-searcher**

#新建程序根文件夹
```
mkdir /opt/book-searcher/
mkdir /opt/book-searcher/index
```
#首页→文件管理器→设置→用户管理→目录范围(留空)→保存

#找到文件夹 /opt/book-searcher/

#打开index，上传index文件( 最好一个一个上传，有单个文件大小限制)

#从本地下载对应book-searcher程序，上传到/opt/book-searcher/

> [armv7架构](https://github.com/bigmouse0001/book-searcher/releases/download/0.9.1.1/book-searcher-armv7-unknown-linux-gnueabihf.tar.gz)
> [arm64/v8架构](https://github.com/bigmouse0001/book-searcher/releases/download/0.9.1.1/book-searcher-aarch64-unknown-linux-musl.tar.gz)

#终端输入nohup ./book-searcher run，按ctrl+c，再输入sudo netstat -tulpn，查看7070端口是否被监听。

#book-searcher添加开机自启，后台运行，异常关闭自启

1. 打开文件管理器，找到 /etc/systemd/system/，新建文件book-searcher.service，并打开
2. 写入以下内容，保存并关闭
```
[Unit]
Description=Book Searcher Service
After=network.target

[Service]
Type=simple
ExecStart=/opt/book-searcher/book-searcher
Restart=always
User=root
Group=root

[Install]
WantedBy=multi-user.target

```

3. 回到终端，输入以下代码，
```
sudo systemctl daemon-reload
sudo systemctl start book-searcher
sudo systemctl enable book-searcher
```
4. 重启机器，终端输入`sudo netstat -tulpn`，查看7070端口是否被监听，如监听，则成功。但需要内网穿透才可正常访问。


**五、安装halo博客**
```
docker run \
  -it -d \
  --name halo \
  -p 8090:8090 \
  -v ~/.halo2:/root/.halo2 \
  halohub/halo:2.5 \
  --halo.external-url=http://localhost:8090/ \
  --halo.security.initializer.superadminusername=admin \
  --halo.security.initializer.superadminpassword=P@88w0rd
```
浏览器打开 ip+8090，内网穿透转发8090端口

**六、安装onenav导航站**

```
docker run -itd --name="onenav" -p 8070:80 \
    -v /data/onenav:/data/wwwroot/default/data \
    helloz/onenav:0.9.30
```
浏览器打开 ip+8070，内网穿透转发8070端口

七、安装komga图书管理

八、安装koodo reader
