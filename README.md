
最近开始把之前一直吃亏的旧电脑拿出来再利用了，先还是选择了熟悉的ubuntu系列。安装了Ubuntu 22\.04之后，风风火火地把需要的开发环境搭建起来，虽然桌面有些卡顿，但瑕不掩瑜玉。趁着热情又想着把它升级到24\.04。结果不巧在升级过程中遇到了网络中断，导致内核模块破碎，重启之后无法顺利进入系统界面。最后走头无路只好重新安装了系统，这个时候已经对Ubuntu系统产生了一些怨念，在终端安装软件的时候也发现了商业硬广，彻底对高版本的Ubuntu失去了好感。
Linux的发行版很多，重新选择一个吧。在知乎上逛了不久，发现了3个选择：


* 1. ArchLinux
* 2. Linux Mint
* 3. Deepin


ArchLinux，这个是一个非常高度定制化的操作系统，可以玩出很多花样，可能年轻心理的极客更喜欢折腾。它支持滚动更新，并且很容易折腾坏系统。。我个人是追求稳定的系统环境的，也过了喜欢整夜不睡觉去折腾的年纪，首先被我排除了。


而Linux Mint是Ubuntu的一个开源分支系统，被广大社区技术爱好者维护和支持，迁移成本最低，且对硬件要求更友好，GOME方面也更保守，选择了传统的X11,而不是Redhat主导的Wayland。这样能保证桌面的稳定性和响应性能更有保证，特别是对于老机型和低配置。


最后一个是Deepin，国产操作系统，它和Ubuntu一样，都是基于Debian系统衍生而来。有非常强大的软件源，对国内软件需求强的人非常友好。最近国家也大力发展国产软件和国产操作系统，在统信发展之下，微信、QQ、飞书等软件都做了Deepin的版本的客户端，让Linux更适合日常国内环境的办公。


我先尝试了Linux Mint，发现卡顿依然存在，而且桌面UI颜值很低。于是又切换到了Deepin，我安装的是目前最新的V 23社区版，一用之下就爱上了这个高颜值、桌面GUI响应流畅的系统。日常国内的办公软件都躺在官方的应用商店里面，任君下载安装。


在搭建开发环境的时候，我发现安装Docker遇到了一定困难。按照官方文档所说，需要去添加APT源，但由于Deepin已经是魔改之后的Debian，它的系统版本名不属于任何Debian。在终端通过命令“cat /etc/os\-release”可以查看系统版本：



```
PRETTY_NAME="Deepin 23"`
`NAME="Deepin"`
`VERSION_ID="23"`
`VERSION="23"`
`ID=deepin`
`HOME_URL="https://www.deepin.org/"`
`BUG_REPORT_URL="https://bbs.deepin.org"`
`VERSION_CODENAME=beige`

```

可以看出Deepin的系统发布版本名称是“beige”，在docker发布的对应的debain的源里面找不到，于是我换成一个比较新的Debian版本名即可，例如bookworm。


所以需要修改命令如下所示：



```

echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "bookworm")" stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

```

然后再更新源：



```
sudo apt update

```

然后再安装docker相关组件：



```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```

然后就可以在终端里面快乐地使用Docker啦！


国产操作系统必须支持，总体上体验很好，对从Windows迁移过来也非常无痛。作为Ubuntu长期使用者，完全无缝切换到了Deepin，先作为个人主力系统来玩起来！


 本博客参考[wgetCloud机场](https://tabijibiyori.org)。转载请注明出处！
