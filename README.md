# 微星 GP76 10th hackintosh

## Msi GP76 10th Hackintosh
### 适用：`2020款微星 GP76,可能还适用于同样 10th 的 GS/GL/GP/GE系列,未测试`
## 电脑配置
|规格 | [详细信息]([https://item.lenovo.com.cn/product/1007854.html](https://www.msi.com/Laptop/GP76-Leopard-10UX/Specification)) |
|:-: | :-:|
|电脑型号|GP76 Leopard 10UG|
|操作系统|macOS （Sonoma (`更早的版本未测试`) |
|处理器|英特尔 酷睿 i7 - 10870H|
|内存|16GB*2|
|硬盘|acer GM7000 2TB/PM981 1TB 已禁用/970EVOplus已拆|
|显卡|Intel HD Graphics UHD630）/Nvidia RTX 3070 Mobile已禁用|
|显示器|17.2 inch IPS 1920x1080|
|声卡| Realtek ALC298/layoutid 30|
|网卡|[原装网卡AX210] ( [Intel网卡](https://github.com/daliansky/XiaoXinPro-13-hackintosh/wiki/Intel%E7%BD%91%E5%8D%A1))|

## 功能部分
|功能 |型号 |状态|备注| 
|:-: | :-:|:-: | :-:|
|核显| UHD 630|`OK`|完美驱动|
|独显| RTX3070m|`Disabled`| 禁用以省电|
|声卡| ALC298|`OK`| layoutID 30|
|无线网卡| inter ax210|`OK` | 挑路由器,不一定好连|
|蓝牙| inter|`OK` | [参照配置说明](https://openintelwireless.github.io/IntelBluetoothFirmware/)|
|睡眠唤醒 | :-:|`OK`| :-:|
|硬盘| GM7000|`OK` | :-:|
|硬盘| PM981(a)|`Disable` | 随机卡死|
|硬盘| 970EVO plus|`Disable` | 随机卡死|
|引导| 只能单系统|-- | 按 F11 用系统引导菜单切换吧|


## 安装部分

混搭硬盘: （`黑苹果下：可用、不可用`）

- `不可用`：PM981|970EVO plus|随机出现硬盘卡顿,特别是保存文件的时候转圈圈,必须启用 SSDT-DNVME.aml禁用
- `可用`：ACER GM7000 2TB 可用,卡顿是因为 PM981A 的问题,这是坑点,我的 8 个小时就是这么过来的,混杂着多系统引导问题[来源 1](https://github.com/neophack/tongfang-utility/blob/cbc091a6880576070d1700cf289d08fe109827f0/src/resources/i18n/config.ts#L86) [来源 2](https://github.com/neophack/tongfang-utility/blob/cbc091a6880576070d1700cf289d08fe109827f0/src/resources/i18n/config.ts#L86)

`PS`: 以上是已知道型号，倘若还有其他型号：既不代表可用，也代表不可用！

BIOS 设置部分:
- `关闭快速启动`
- `关闭安全引导`

安装过程:(略)

## 安装后执行的操作
此处来源于[黑果小兵博客](blog.daliansky.net)

- `启用macOS安装应用允许任何来源`
sudo spctl --master-disable
- `内存供电，内存镜像不写入硬盘`
sudo pmset -b hibernatemode 0
- `关闭被同一 iCloud 下的设备唤醒`
sudo pmset -b acwake 0
- `关闭雷电固件更新`
sudo softwareupdate --ignore ThunderboltFirmwareUpdate1.2
- `为第三方硬盘启用 TRIM`
sudo trimforce enable 
- `安装 homebrew`
pwpolicy -clearaccountpolicies
- `取消四位数密码限制`
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## 坑点教训
- 坑点 1 `PM981/970EVO plus的随机卡死问题`,保存文件很卡,卡了又会好,一直以为是 GM7000的问题,最好才找到提示说随机卡死问题,我的 8 小时.感谢[来源 1](https://github.com/neophack/tongfang-utility/blob/cbc091a6880576070d1700cf289d08fe109827f0/src/resources/i18n/config.ts#L86) [来源 2](https://github.com/neophack/tongfang-utility/blob/cbc091a6880576070d1700cf289d08fe109827f0/src/resources/i18n/config.ts#L86)
- 坑点 2 `声音问题`,加减声音图标正常,尝试了一堆 ID,尝试了 fix_IRQ,尝试了 azml->HDEF,然后发现是系统界面没开声音调节反馈,我的 4 小时.
- 坑点 3 `USB 定制导致卡 Applekeysupport fail,这个是因为英特尔蓝牙驱动注入方式变了,还有就是可能是英特尔无线网卡,这两个先禁用就能正常安装,[配置参考](https://openintelwireless.github.io/IntelBluetoothFirmware)
- 坑点 4 `多系统引导`这个我到现在没找到问题所在,所以解决不了,还是用 F11系统菜单选择其他系统选项吧,可以配合 easyUEFI 或 bootice 食用.
- 坑点 5 `信息检索`中文互联网,有用的信息蛮少,呵呵哒!

## 最后来点靓照吧

