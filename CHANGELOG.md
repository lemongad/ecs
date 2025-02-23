# CHANGELOG

# 主要变化

2023.05.11 删除当识别为中国IP时仍然检测线路和回程路由的部分，准备替换为全国省会的Ping值检测

2023.05.06 网站 ipinfo.io 的API有的机器因为代理原因或同段欺诈分过高原因，免费的额度耗尽，修复自动替换为其他接口查询，修复查询开发板的CPU型号时有换行符的问题

2023.05.05 部分服务器在测试时使用speedtest-cli组件版本有要求，修复自动替换版本时部分服务器重复测试的问题

2023.05.04 优化io测试中重复查询系统信息以及CPU检测时重复查询系统版本的函数，修改部分分区描述，修复在开发板上的本地设备检测不到CPU型号的问题

2023.05.03 修复三网路由测试显示ASN时不显示AS号码的问题，删除无效的全国网络延迟测试

2023.05.02 修复纯IPV6无法测试四网线路显示文件不存在的问题，修复纯IPV6网络查询到的ASN只显示了名字没显示AS号码的问题，修复IPV4的ASN查询可能出现的bug，增加两个数据来源网站

2023.05.01 修复部分ARM机器识别CPU成功，但在甲骨文的新加坡的ARM上，即便使用yabs的CPU检测依然无法检测CPU类型的问题，修复显示ASN组织时使用ip.sb源时不显示AS号码的问题，删除上传的结果中yabs的IO测试部分出现的一些无效行，修复分区选择时可能错按选项导致菜单退出的问题，合并三网路由检测的函数简化代码

2023.04.29 修复纯IPV6机器的IPV6测试中可能存在的一些BUG，修复纯IPV6机器的IPV6的ASN有时候识别失效的问题

2023.04.29 修复部分机器查询内容的free命令不存在的问题，修复部分机器/proc/sys/vm/drop_caches是只读权限时，清除内存缓存会报无法写入的错误，增加sudo组件的检测和安装，修补有时候docker容器内的虚拟化架构检测误判为宿主机虚拟化架构的问题

2023.04.28 第三方脚本区新增全球测速脚本，对应speedtest.cn的三网测速脚本，修复部分服务器组件安装需要交互的问题

2023.04.27 修复单项测试多下载了io测试文件的问题，修复可能的非英文语言系统造成的部分信息识别失效的问题，修复screen挂起时语言模块缺少en_utf8语言包显示乱码的问题

2023.04.25 更新修复国内服务器测三网路由时下载出错的问题

2023.04.24 检测国内外IP增加两个判断，避免在国内还继续测流媒体等无用信息，修补使用CDN下载可能造成的重定向跟踪问题

2023.04.15 使用[ecs-net](https://github.com/spiritLHLS/ecsspeed)自写测速脚本替代原有的脚本，修改：
- 三网测速每个运营商选择本机ping值最低的两个节点测速，节点列表大概每7天自动更新一次
- 支持国内服务器测试(有判断是否为国内机器)，在国内使用时使用CDN加速
- 当官方CLI安装失败(如罕见的架构或者官方网站访问失败时)自动使用 speedtest-go 作为替代品测速
- 同时修改了一个融合怪并发测试的版本，追求更短的测试时长，但前提要求是机器足够强劲

2023.04.14 去除Python3的依赖，全套脚本只使用Shell语言，IPV4的检测使用多个数据来源，保证IP质量检测能正常运行，不仅限于ip.sb来源，删除一个无效的IP数据库来源，去除jq组件和python组件的依赖，大幅度减少前期组件安装所需的时间

2023.04.13 修复检测ARM时CPU识别不出来的BUG

2023.04.12 修复如果测试有问题出现空测评的情况时会传空文件到pastebin的问题，增加Geekbench6测试选项在对应分区

2023.04.03 修复sjlleo的nf查询不支持ARM架构机器查询的问题，但考虑到sjlleo不再维护流媒体检测的脚本，考虑替换别的作者的脚本检测

2023.04.02 修复脚本openai脚本测试超时的问题，使用自维护的脚本，第三方流媒体检测方面脚本加入本人优化版本的选项，运行完毕自动上传结果到pastebin并给出分享链接

2023.03.30 脚本运行还没选择就进行了部分组件的安装的逻辑问题已解决，组件只在选择完毕后进行安装，删除无效的ping0数据库，增加ip234数据库，优化了IP质量查询的函数减少了模块依赖，替换IP质量检测的V6检测平台，支持V6的地址进行检测，升级sysbench由1.0.17到1.0.20版本

2023.03.12 更新修复适配中文系统支持，解决部分命令查询结果为中文不适配，更新了移动的测速节点ID

2023.03.04 使用tmp文件优化缩减脚本执行时长，缩减了大概30秒执行时长

2023.02.28 修复纯V6网络测试容易触发的某些错误

2023.02.20 修复Fedora 23系统检测被redhat检测覆盖的问题，修复debian/ubuntu低版本需要验证才能下载virt-what, jq等工具包的问题

2023.02.11 新增OpenAI检测，已加入融合怪套餐，修复删除部分流媒体检测空行的显示节省空间

2023.02.08 解决almalinux部分版本安装不上sysbench部件的问题(epel-release的编译安装新增almalinux的判断)

2023.02.06 解决almalinux不自带unzip的问题

2023.01.25 IP质量检测重构输出，增加两个数据库来源

2023.01.20 三网路由测试收纳 nexttrace 作为第三方脚本选项和原创区脚本选项

2023.01.19 修复自定义IP路由测试的一些显示bug

2023.01.17 硬件测试合集添加对应硬件测试脚本，修改部分链接使用原始链接。

2023.01.16 隐藏部分错误显示，优化了输出。

2023.01.15 更新tiktok的检测，替换失效的函数

2023.01.14 新增成都三网回程路由测试选项，改进测速部分的显示去除乱码，优化代码缩减了代码行数。

2023.01.11 由于部分新服务器刚开机不自启动bbr，现脚本询问是否需要启动了bbr后再进行测试(前提是服务器自身已安装bbr但未启动，未安装则不询问，已启动也不询问)，第三方脚本重新分区并整合为合集，相同类型脚本在同合集中，自行选择，部分脚本描述细微更改

2023.01.07 删除部分无效代码，三网回程路由优化使用ip.sb进行IP检测与ASN检测，再度优化缩减代码行数，merge了一个push以支持arch系统测试

2023.01.06 修复IP质量检测的curl有的服务器会curl到V6去，而不是最基础的V4的bug，merge一个pull，脚本支持arch系统测试了

2023.01.03 更改三网回程的环境文件下载方式，避免某些隐性bug

2023.01.02 下载环境前预加载CDN加速轮询判断，如若无可用CDN才用原链接，解决国内服务器无法访问部分资源的问题，加速各种环境文件的下载，减少脚本环境准备时长。

2023.01.01 修复脚本部分curl命令需要ssl验证的问题，已忽略校验，修复脚本OVZ运行时执行内核缓存清除报错显示的问题，修复python2版本不做IP质量检测以达到修复执行报错的问题，修复如果未设置TCP拥堵控制算法时显示为空的问题。

2022.12.28 修复查询TCP加速方式时可能遇到的sysctl的路径不存在或者异常的问题，修复虚拟化架构只通过命令判断有可能失效导致查询结果为Dedicated的问题，增加检查系统文件的查询函数，简化部分函数判断，缩减脚本行数

2022.12.17 删除一个无效数据库来源，又套了cf的5秒盾了，啧

2022.12.14 非致命性bug后续很长一段时间内不再更新本脚本，所有致命性bug已修复，第三方脚本增加两个三网回程线路检测脚本，原创区新增自定义IP的IP质量检测脚本，融合怪的执行结果保存在```/root```下的test_result.txt中，运行完毕可用```cat test_result.txt```查看记录

2022.12.13 流媒体检测部分远程调用最新脚本不再直接使用老脚本函数，检测准确度提升，替换部分github的raw链接使用cf的cdn链接加速下载，融合怪脚本所需运行时长缩减

2022.12.12 新增两个IP类型数据库，IP检测已包含三个数据库，修复debian10系统apt源broken的问题，内置```apt --fix-broken install -y```，修复centos8的源失效问题，自动替换新源下载```AppStream```，新增支持Almalinux系统

2022.12.11 不再使用ip.gs改用api.ipify.org进行IP识别

2022.11.04 更新替换Tiktok检测脚本为superbench脚本，暂时移除端口检测，第三方脚本增加Geekbench选项，修改部分分区描述

2022.10.02 重新划分测试区域，含借鉴脚本的原始脚本选项和原创脚本选项，如果本脚本不好用，可以试试原始脚本

2022.09.23 增加全国网络延迟测试，新增两个原始版本的三网测速的选项

2022.08.31 增加三网路由延迟，Tiktok解锁测试提速
