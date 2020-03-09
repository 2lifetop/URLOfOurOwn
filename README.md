# URL of Our Own
URL of Our Own 是 [archiveofourown.org (下称 AO3)](https://archiveofourown.org) 的一个反向代理项目, 有时称其为镜像站.

该项目意在帮助各位创作者自由的进行创作, 提供在特殊网络环境下的 AO3 访问.

_如果您觉得它不能称之为一个"项目", 您可以直接提交PR修改这个称呼, 反正我管它叫项目_

## 如何使用?
直接访问 [urls.jsonc](https://github.com/ExcitedCodes/URLOfOurOwn/blob/master/urls.jsonc) 中 "available" 一节下的任意域名即可

比如, 您看到了下面的内容, 则直接访问 [ao3.wtf](https://ao3.wtf) 即可
```jsonc
{
	"available": [
		"ao3.wtf"
	],
	"blocked": []
}
```

## 如何搭建?
1. 首先, 您需要准备一个在目标地区可以正常解析域名和一个能访问到 AO3 的服务器
   *
   * _我们建议您使用主流 Linux 发行版, 如 Ubuntu、CentOS 等_
   * _我们建议您到 __提供 Whois Proxy(又称 Whois Privacy, 域名隐私保护, WhoisGuard 等) 服务的国外域名注册商__ 注册域名并开启 Whois Proxy_
   * _我们建议您到 [Cloudflare](https://cloudflare.com/) 申请一个账户并添加您的域名 ([官方文档](https://support.cloudflare.com/hc/zh-cn/articles/201720164-%E5%88%9B%E5%BB%BA-Cloudflare-%E5%B8%90%E6%88%B7%E5%B9%B6%E6%B7%BB%E5%8A%A0%E7%BD%91%E7%AB%99))_
2. 接下来, 在您的服务器上安装必要软件
   * [Nginx](https://nginx.org/),  请参阅 [安装Nginx](#%E5%AE%89%E8%A3%85-nginx) 一节
   * Git, Vim 等
      * Ubuntu: `sudo apt install -y git vim`
      * CentOS: `sudo yum install -y git vim`
3. 从我们的存储库下载所需的文件, 在任意路径执行 `git clone https://github.com/ExcitedCodes/URLOfOurOwn.git`
4. 准备 Nginx 配置文件, 执行 `sudo cp URLOfOurOwn/proxy/nginx/* /etc/nginx/conf.d`
5. 准备一个放置代理文件的路径, 您可以直接执行 `sudo cp -r URLOfOurOwn/proxy/ao3 /var/www/html/ao3`
   * 注意调整文件权限, 执行 `sudo chmod -R 755 /var/www/html/ao3`
6. 修改配置文件使其符合您的域名, __请全程使用英文输入法并注意不要误删分号__, 执行 `sudo vim /etc/nginx/conf.d/site.conf`
   * 按一下 i 进入编辑模式, 您应该会注意到左下角出现 `-- INSERT --` 字样
   * 在第3行左右找到 `server_name <Fill_Domain>;` 并将其替换为您的域名, 如 `server_name  ao3.wtf;`
   * 在第18行左右找到 `root <Fill_AO3>;` 并将其替换为第5步中的路径. 如果您直接执行了那行路径, 请填写 `/var/www/html/ao3`
   * 此处暂时不提供配置缓存的教程, 因为 AO3 的登录态会被附加在页面中
   * 如果您 __不__ 使用 Cloudflare:
     * 找到 `$http_cf_connecting_ip` 并替换为 `$remote_addr`
     * 找到文件末尾的 `include conf.d/cloudflare.inc;` 和 `deny all;` 两行并在最前面加上 `#`
   * 配置完毕后按三下 ESC 按键并输入 `:wq`, 按回车退出 vim
7. 接下来, 启动 (或重启) 您的 Nginx, 执行 `systemctl restart nginx`
   * 如果您希望 Nginx 自动启动, 请执行 `systemctl enable nginx`
8. 将您的域名解析到您的服务器
9. 现在, 您的代理网站应该可以工作了. 尝试在浏览器中访问它, 如果它工作并且您愿意与我们共享这一域名, 我们建议您到 [此处](https://github.com/ExcitedCodes/URLOfOurOwn/issues) 提交您的域名

### 安装 Nginx
暂时只提供 Linux 下的安装简介
* Ubuntu 18.04:
   * [详细教程](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)
   * 简化版:
     ```console
     $ sudo apt update
     $ sudo apt install nginx
     $ sudo ufw allow 'Nginx HTTP'
     ```
 * CentOS 7:
   * [详细教程](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7)
   * 简化版:
     ```console
     $ sudo yum install epel-release
     $ sudo yum install nginx
     $ sudo firewall-cmd --permanent --zone=public --add-service=http
     $ sudo firewall-cmd --reload
     ```
