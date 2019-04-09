# sogo

一个使用http流量进行混淆的socks5代理。

服务器端：[sogo-server](https://github.com/arloor/sogo-server)

## 运行日志

以下是观看一个youtube视频的日志：

```shell
2019/04/10 00:14:28 main.go:58: 与客户端握手成功
2019/04/10 00:14:28 main.go:207: 目的地址类型:3 域名长度:15 目标域名:www.youtube.com 目标端口:443
2019/04/10 00:14:28 main.go:58: 与客户端握手成功
2019/04/10 00:14:28 main.go:207: 目的地址类型:3 域名长度:11 目标域名:i.ytimg.com 目标端口:443
2019/04/10 00:14:28 main.go:58: 与客户端握手成功
2019/04/10 00:14:28 main.go:207: 目的地址类型:3 域名长度:13 目标域名:yt3.ggpht.com 目标端口:443
2019/04/10 00:14:35 main.go:58: 与客户端握手成功
2019/04/10 00:14:35 main.go:207: 目的地址类型:3 域名长度:32 目标域名:r2---sn-i3belnel.googlevideo.com 目标端口:443
2019/04/10 00:14:35 main.go:58: 与客户端握手成功
2019/04/10 00:14:35 main.go:207: 目的地址类型:3 域名长度:32 目标域名:r2---sn-i3belnel.googlevideo.com 目标端口:443
2019/04/10 00:14:35 main.go:58: 与客户端握手成功
2019/04/10 00:14:35 main.go:207: 目的地址类型:3 域名长度:32 目标域名:r2---sn-i3belnel.googlevideo.com 目标端口:443
```

以下是访问github的日志：
```shell
2019/04/10 00:15:57 main.go:58: 与客户端握手成功
2019/04/10 00:15:57 main.go:207: 目的地址类型:3 域名长度:10 目标域名:github.com 目标端口:443
2019/04/10 00:15:57 main.go:58: 与客户端握手成功
2019/04/10 00:15:57 main.go:207: 目的地址类型:3 域名长度:10 目标域名:github.com 目标端口:443
2019/04/10 00:15:59 main.go:58: 与客户端握手成功
2019/04/10 00:15:59 main.go:207: 目的地址类型:3 域名长度:15 目标域名:live.github.com 目标端口:443
2019/04/10 00:16:00 main.go:58: 与客户端握手成功
2019/04/10 00:16:00 main.go:207: 目的地址类型:3 域名长度:14 目标域名:api.github.com 目标端口:443
```

## 核心

核心就是sogo与sogo-server之间的流量全都伪装成了http流量。即payload外包裹http请求/响应的头。

另一个重要的点是，识别到sogo-server的非sogo客户端的http请求。当收到这种请求时，这时会像一个“反向代理”一样，将所有流量转发到预先设好的网站。因此，直接访问 http://sogo-server-ip:80，将会显示这个被“反向代理”的网站。
