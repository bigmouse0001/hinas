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

`docker run -d --restart=always -p 7070:7070 ghcr.io/little-boypp/book-searcher:0.9.1.2`

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

账号：admin
密码：P@88w0rd
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
