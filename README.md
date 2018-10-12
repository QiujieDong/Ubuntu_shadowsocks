# Ubuntu_shadowsocks

ubuntu系统需要安装shadowsocks,捣鼓了好长时间终于弄好了,写下来:

我的ubuntu是18版的.

安装:
我安装的是客户端版本:https://github.com/shadowsocks/shadowsocks-qt5

在终端中运行下面三句命令:

sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
当运行第一句时,出现错误:
使用sudo add-apt-repository ppa:hzwhuang/ss-qt5命令添加ppa源时出现错误
错误:10 http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu bionic Release
  404  Not Found [IP: 91.189.95.83 80]
正在读取软件包列表... 完成
E: 仓库 “http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu bionic Release” 没有 Release 文件。
N: 无法安全地用该源进行更新，所以默认禁用该源。
N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。

解决办法:
在/etc/apt/sources.list.d目录下，找到文件(hzwhuang-ubuntu-ss-qt5-bionic.list )将里面的bionic 改成xenial ,保存再运行 sudo apt-get update ,最后再运行一次 sudo apt-get install shadowsocks-qt5 就好了。
因为在ppa:hzwhuang/ss-qt5 并没有18.04版本的源，所以再执行update时会出现这个错误。

这时候客户端版应该安装成功了,下面看看配置:
1.打开客户端版,自己可以从gui-config.json导入配置信息,也可以手动设置,最好是勾选"程序启动时自动连接"

2.要浏览器等使用还需要配置网络代理:

终端运行(如果已经安装了pip,可以跳过这一步):

apt-get install python-pip
下载genpac:

sudo pip install -i https://pypi.douban.com/simple genpac
生成pac文件(默认生成的文件位于home/用户名下):

genpac --pac-proxy "SOCKS5 127.0.0.1:1080" --output="autoproxy.pac"

3.打开ubuntu系统的:设置-网络-网络代理,设置为"自动",将上面生成的pac文件的路径复制到"配置URL"中

这里需要说明的是，路径复制到URL时，格式为：file:/+你的路径，例如我的是：

file:///home/abc/snap/Shadows/autoproxy.pac

 

配置完成后,这时候打开客户端,在运行就可以使用了.
--------------------- 

