# ecs

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FspiritLHLS%2Fecs&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

### 前言

如果脚本有任何问题或者任何修复系统的需求，可在issues中提出，有空会解决或者回答

支持系统：Ubuntu 18+，Debian 8+，centos 7+，Fedora 22+，Almalinux 8.5+, Arch

# 目录
 * [融合怪测评脚本](#融合怪测评脚本)
    * [交互形式](#交互形式)
    * [无交互形式](#无交互形式)
    * [说明](#说明)
 * [纯测IP质量](#纯测IP质量)
 * [部分服务器运行测试有各类bug一键修复后再测试](#部分服务器运行测试有各类bug一键修复后再测试)
 * [待解决事项](#待解决事项)
 * [更新](#更新)
 * [功能](#功能)
 * [友链](#友链)
    * [测评频道](#测评频道)
    * [自动更新测速服务器节点列表的网络基准测试脚本](#自动更新测速服务器节点列表的网络基准测试脚本)
 * [脚本概况](#脚本概况)
 * [致谢](#致谢)

<a id="top"></a>
------
<a id="artical_1"></a>

### 融合怪测评脚本

#### 交互形式

```bash
curl -L https://gitlab.com/spiritysdx/za/-/raw/main/ecs.sh -o ecs.sh && chmod +x ecs.sh && bash ecs.sh
```

或

```bash
curl -L https://github.com/spiritLHLS/ecs/raw/main/ecs.sh -o ecs.sh && chmod +x ecs.sh && bash ecs.sh
```

或

```
bash <(wget -qO- bash.spiritlhl.net/ecs)
```

#### 无交互形式

```bash
echo 1 | bash <(wget -qO- --no-check-certificate https://gitlab.com/spiritysdx/za/-/raw/main/ecs.sh)
```

或

```bash
echo 1 | bash <(wget -qO- --no-check-certificate https://github.com/spiritLHLS/ecs/raw/main/ecs.sh)
```

或

```
echo 1 | bash <(wget -qO- bash.spiritlhl.net/ecs)
```

#### 说明

融合怪的执行结果保存在当前路径下的test_result.txt中，运行完毕可用```cat test_result.txt```查看记录

融合怪的完整版和精简版运行完毕自动上传结果到pastebin并回传分享链接

融合怪测试说明以及部分测试结果的内容解释(初次使用推荐查看)：
<details>

除了已标注的原创内容，其余所有分区均为借鉴并进行优化修改后的版本，与原版本基本都不大一样

系统基础信息测试融合了三家还有我自己修补的部分检测(systl和virt)，应该是目前最全面的了

CPU测试使用sysbench测试得分，不是yabs的gb4或gb5，前者只是简单的计算质数测试速度快，后者geekbench是综合测试系统算加权得分，不是同一种东西，别互相比较了，没有任何用处

CPU测试单核得分在5000以上的可以算第一梯队，4000到5000分算第二梯队，每1000分算一档，自己看看自己在哪个档位吧

AMD 7950x单核满血性能得分在6500左右，AMD 5950x单核满血性能得分5700左右，Intel普通的CPU(E5之类的)在1000~800左右，低于500的单核CPU可以算是比较烂的了

IO测试收录了两种，来源于lemonbench的dd磁盘测试和yabs的fio磁盘测试，综合来看会比较好，前者可能误差偏大但测试速度快无硬盘大小限制，后者真实一点但测试速度慢有硬盘以及内存大小要求

流媒体测试收录了两种，一个是go编译的二进制文件和一个shell脚本版本，二者作者有独到之处，互相对比看即可

tiktok测试有superbench和lmc999两种版本，哪个失效了随时可能更新为其中一种版本，以最新的脚本为准

回程路由测试选用的GO编译的二进制版本和朋友pr的版本，本人只做了优化适配多个IP列表

IP质量检测纯个人原创，如有bug或者更多数据库来源可在issues中提出，日常看IP2Location数据库的IP类型即可

融合怪的IP质量检测是简化过的，没有查询Cloudflare的威胁得分，个人原创区的IP质量检测才是完整版(或者仓库说明中列出的那个IP质量检测的命令也是完整版)

三网测速使用自写的测速脚本，尽量使用最新节点最新组件进行测速，且有备用go版本测速，做到自更新测速节点列表，自适应系统环境测速

其他第三方脚本归纳到了第三方脚本区，里面有同类型脚本不同作者的各种竞品脚本，如果融合怪不能使你满意或者有错误，可以看看那部分

原创脚本区是个人原创的部分，有事没事也可以看看，可能会更新某些偏门或者独到的脚本

VPS测试，VPS测速，VPS综合性能测试，VPS回程线路测试，VPS流媒体测试等所有测试融合的脚本，本脚本能融合的都融合了

</details>

**有时候想要测一些配置极其拉跨的机器时，推荐使用screen挂起执行融合怪**

**然后你可以关闭SSH连接，等待一段时间后使用```cat test_result.txt```查看运行的实时状况**

**这样可以避免IO或者CPU过于垃圾导致的测试过程中的SSH连接中断，就不会测一半啥都没了**

最烂机器测试的例子(跑了47分钟一样测完)：[跳转](https://github.com/spiritLHLS/ecs/blob/main/lowpage/README.md)

使用**CDN**加速理论上已支持**国内**和**国外**服务器测试，但国内受CDN口子或国内机器口子的限制会加载慢很多

**[返回顶部](https://github.com/spiritLHLS/ecs#top)**

### 纯测IP质量

- IP黑 ```OR``` 白
- 含IPV4 ```AND``` IPV6

```bash
bash <(wget -qO- --no-check-certificate https://gitlab.com/spiritysdx/za/-/raw/main/qzcheck.sh)
```

或

```bash
bash <(wget -qO- --no-check-certificate https://github.com/spiritLHLS/ecs/raw/main/qzcheck.sh)
```

### 部分服务器运行测试有各类bug一键修复后再测试

一键修复各种系统原生bug的仓库：

https://github.com/spiritLHLS/one-click-installation-script

如若还有系统bug请到上面仓库的issues反映，脚本原生BUG该仓库issues反映

# 待解决事项

三网回程测试基于 ipip.net 的程序，似乎有时区要求或者时间准确度要求，待检测修正避免出现 timestamp error 的错误报告 - 待修复

ARMV7l的机器测IO时会失效，yabs和lemonbench的测试均失效 - 待修复

端口检测(检测是否被墙) - 待修复

全国/全球网络延迟测试 - 待修复

# 更新

2023.05.13 增加全国三网ping值测试的脚本，指定检测到中国IP时使用延迟检测替换路由检测，增加可用的CDN(自建白名单CDN)，增加中国IP检测的API(cip.cc)，增加第三方脚本添加三网Ping值测试脚本

历史更新日志：[跳转](https://github.com/spiritLHLS/ecs/blob/main/CHANGELOG.md)

**[返回顶部](https://github.com/spiritLHLS/ecs#top)**

# 功能

- [x] 自由组合测试方向和单项测试以及合集收录第三方脚本--原创
- [x] 基础系统信息--感谢teddysun和superbench和yabs开源，本人修改整理优化
- [x] CPU测试--感谢lemonbench开源，本人修改整理优化
- [x] 内存测试--感谢lemonbench开源
- [x] 磁盘IO读写测试--感谢lemonbench开源，本人修改整理优化
- [x] 硬盘IO读写测试--感谢yabs开源[项目](https://github.com/masonr/yet-another-bench-script)，本人修改整理优化
- [x] 御三家流媒体解锁测试--感谢sjlleo的[二进制文件](https://github.com/sjlleo?tab=repositories)，本人修改整理优化
- [x] 常用流媒体解锁测试--感谢RegionRestrictionCheck的[项目](https://github.com/lmc999/RegionRestrictionCheck)，本人修改整理优化
- [x] Tiktok解锁--感谢lmc999的[项目](https://github.com/lmc999/TikTokCheck)，本人修改整理优化
- [x] OpenAI检测--感谢missuo提供的[项目](https://github.com/missuo/OpenAI-Checker)，本人修改整理[优化项目](https://github.com/spiritLHLS/OpenAI-Checker)，去除很多BUG
- [x] 三网回程以及路由延迟--感谢zhanghanyun/backtrace开源[项目](https://github.com/zhanghanyun/backtrace)，本人修改整理
- [x] 回程路由以及带宽类型检测(商宽/家宽/数据中心)--由fscarmen的PR以及本人的技术思路提供，本人修改整理优化
- [x] IP质量检测(检测IP白不白)(含IPV4和IPV6)--本人独创，感谢互联网提供的查询资源
- [x] speedtest测速--使用自写[ecs-net](https://github.com/spiritLHLS/ecsspeed)脚本，自动更新测速服务器ID，一劳永逸解决老是要手动更新测速ID的问题
- [ ] 端口检测(检测是否被墙)--由fscarmen的PR以及本人的技术思路提供 - 待修复

# 友链

## 测评频道

### https://t.me/vps_reviews

## 自动更新测速服务器节点列表的网络基准测试脚本

### https://github.com/spiritLHLS/ecsspeed

**[返回顶部](https://github.com/spiritLHLS/ecs#top)**

# 脚本概况

主界面：

![图片](https://user-images.githubusercontent.com/103393591/233968968-e06be6c5-981e-440a-b519-b5d9a219b96a.png)

选项1融合怪完全体：

![图片](https://user-images.githubusercontent.com/103393591/233967406-d2b74a20-8d95-4c18-8df1-254b97942f7d.png)
![图片](https://user-images.githubusercontent.com/103393591/233968402-135c3f5e-def7-4f6e-a113-06d627780323.png)
![图片](https://user-images.githubusercontent.com/103393591/233968486-60ccc9b7-2e4f-4cac-838f-fb4617eb118d.png)
![图片](https://user-images.githubusercontent.com/103393591/233968544-b9d6f9ae-416a-4832-a516-8afb3846e33e.png)
![图片](https://user-images.githubusercontent.com/103393591/233968662-f6174bed-1c72-4385-8716-8e1f9b9c4dce.png)
![图片](https://user-images.githubusercontent.com/103393591/233968669-f58624ba-2611-4232-9326-0ce3e9d02d44.png)
![图片](https://user-images.githubusercontent.com/103393591/233968819-f25086df-b3cd-4103-995a-8cc8512fe89d.png)

选项6原创区：

![图片](https://user-images.githubusercontent.com/103393591/233969037-17d3d8e9-e42e-4314-ab89-13f76ea9fd98.png)

**[返回顶部](https://github.com/spiritLHLS/ecs#top)**

# Stargazers over time

[![Stargazers over time](https://starchart.cc/spiritLHLS/ecs.svg)](https://starchart.cc/spiritLHLS/ecs)

# 致谢

感谢 ipinfo.io ip.sb cheervision.co ipip.net cip.cc 提供的网络检测组件

感谢所有开源项目提供的原始测试脚本

同时感谢以下平台

![PyCharm logo](https://resources.jetbrains.com/storage/products/company/brand/logos/PyCharm.png)

**[返回顶部](https://github.com/spiritLHLS/ecs#top)**
