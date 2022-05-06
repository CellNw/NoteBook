# Manjaro 安装教程

## 启动盘制作

> 以下操作均在 Win10 下完成。

1. 进入 [Manjaro 官网](https://manjaro.org/download/)下载镜像，本人所使用的是 `KDE` 桌面环境，因为 `KDE` 对 hidpi 支持比较好。
2. 使用`refus` 制作启动盘，[官网](https://rufus.ie/zh/)。
3. 清理优盘（此操作会清除优盘中所有内容！注意备份！），按`Win + R`，输入 `diskpart`。输入 `list disk` 查看用来安装系统的优盘是第几号，然后输入 `select disk <你的优盘编号>`，输入 `clean` 来清理优盘所有分区，接着输入`convert gpt`，将优盘转化为 `gpt` 分区。
4. 进入打开第二步中下载的`refus`，选择第一步中下载镜像，选择第三步准备好的优盘，点击开始，注意需要使用写入方式为 `dd`。

## 系统安装

1. 关闭安全启动，每个品牌的电脑不一样，自行查阅。
2. 插入优盘，设置优盘为第一启动，每个品牌电脑不一样，请自行查阅。
3. 启动电脑，选择使用开源驱动或者闭源驱动，本人需要运行使用`gpu`做机器学习故只能选择闭源驱动。进入系统后，点击安装系统进入安装界面，这个界面没什么需要注意的除了系统安装位置，不要选错了，其他的选项按照自己的需要选择。

## 必要设置

> 以下操作均在 Manjaro 下完成

1. 如果你的电脑上还有 Windows 系统的话，你会发现两个系统时间不一致，在终端中运行
  ``` shell
  timedatectl set-local-rtc 1 --adjust-system-clock
  ```
2. 设定国内源加快下载速度
  ``` shell
  pacman-mirrors -i -c China -m rank
  pacman -Syyu
  ```
3. 安装`yay`
  ``` shell
  pacman -S yay
  ```
4. 安装具有中国特色的网络工具
  ```shell
  pacman -S v2ray
  yay -S v2raya
  ```
  安装好后打开 http://127.0.0.1:2017/

5. 修改键盘快捷键模式，[参考网址](https://wiki.archlinux.org/title/Apple_Keyboard#Function_keys_do_not_work)
  - 0 禁用功能键，按 ‘Fn’ + ‘F8’ 等同于 F8
  - 1 默认功能键，按 ‘F8’ 触发功能键 (play/pause)，按 ‘Fn’ + ‘F8’ 触发 F8 键
  - 2  默认非功能键，按 ‘F8’ 触发 F8 键，按 ‘Fn’ + ‘F8’ 触发功能键 (play/pause)
  ```
  # vim /etc/modprobe.d/hid_apple.conf
  options hid_apple fnmode=2
  ```