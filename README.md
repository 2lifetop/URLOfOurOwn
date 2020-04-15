
# URL of Our Own
URL of Our Own 是面对 [archiveofourown.org ](https://archiveofourown.org)（下称 AO3）网站 的一个提供反向代理配置的项目。

该项目旨在帮助各位内容创作者自由地进行创作，保障在特殊网络情形下对 AO3 网站的正常访问.

## 如何使用?

演示站点：~[https://ao3.wtf](https://ao3.wtf)~ _(我们采用了全新的边缘计算代理模式, 此项目仍会继续维护但我们不再提供演示站点.)_

### 备用站点

直接访问 [urls.jsonc](https://github.com/2lifetop/URLOfOurOwn/blob/master/urls.jsonc) 中打开 "available" 一节下的任意域名即可（有待后续添加更多）。

例如如下内容，直接访问 [ao3.wtf](https://ao3.wtf) 即可。

```jsonc
{
	"available": [
		"ao3.wtf"
	],
	"blocked": []
}
```

## 如何搭建?

1. 首先，你需要准备一个在目标地区可以正常解析域名和一个能访问到 AO3 的服务器（即位于海外），并且拥有 `root` 访问权限；

   * _我们建议使用主流 Linux 发行版，如 Ubuntu、CentOS 等。_
   * _我们建议使用注册于海外域名注册商，并且开启了域名隐私保护服务的域名作为反代域名。_
   * _我们建议使用 [Cloudflare](https://cloudflare.com) 。申请账户和添加域名请见（[官方文档](https://support.cloudflare.com/hc/zh-cn/articles/201720164-%E5%88%9B%E5%BB%BA-Cloudflare-%E5%B8%90%E6%88%B7%E5%B9%B6%E6%B7%BB%E5%8A%A0%E7%BD%91%E7%AB%99))_

2. 接下来，在你的服务器上安装宝塔面板
前往[面板官方安装教程](https://bt.cn/bbs/thread-19376-1-1.html)
3. 安装好后浏览器进入面板地址再安装NGINX，其余软件可暂时不用安装
4. 解析域名到服务器地址和点击网站-添加站点输入域名即可。创建好后进入网站目录。
5. 下载镜像代码：远程下载——https://github.com/2lifetop/URLOfOurOwn/archive/0.1.zip
6. 解压后将URLOfOurOwn/proxy/ao3/ 下所有文件提取至网站根目录。然后进入网站设置页面
7. 先复制URLOfOurOwn/proxy/nginx/site.conf的配置内容然后申请SSL证书，对网站地址和证书地址等进行修改。
至此大功告成。


```
