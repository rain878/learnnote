# centos

## 下载

# ubuntu

## 下载

# kali

## 下载

## 软件源

```bash
    kali-rolling：使用 KaliLinux的滚动发布（rolling release）版本，即持续更新的版本，不像传统的固定版本发行版
		main：这是软件包的分类。main 包含了由官方 Kali Linux 团队维护和支持的自由软件。
    contrib 表示包含了由Kali Linux社区提供的自由软件，但依赖于非自由软件的库或工具。
    non-free 是包含了非自由软件，这些软件不符合自由软件基金会（Free Software Foundation）的自由软件定义。
    no-free-firmware 表示不包含非自由固件。Kali Linux 重视开源和自由软件，所以这个选项通常用于排除依赖于专有硬件驱动程序的软件包。
		deb 行用于获取已编译的二进制软件包，而 deb-src 行用于获取软件包的源代码
#中科大
deb http://mirrors.ustc.edu.cn/kali/ kali-rolling main non-free contrib #
deb-src https://mirrors.ustc.edu.cn/kali/ kali-rolling main non-free contrib
#阿里云
deb http://mirrors.aliyun.com/kali/ kali-rolling main non-free contrib
deb-src https://mirrors.aliyun.com/kali/ kali-rolling main non-free contrib
#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali/ kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali/ kali-rolling main contrib non-free
#浙大
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
```



# Arch

## 下载

官网[arch](https://archlinux.org/download/)

阿里云下载[arch](https://mirrors.aliyun.com/archlinux/iso)

## 安装

### 手动安装

对磁盘进行分区和挂载

```bash
#查看硬盘
fdisk -l
#选择一个硬盘进行安装
fdisk /dev/sda
#引导分区
n  
+512M
#创建所谓的虚拟分区(swap)
n
+2G
#创建主分区
n
#格式化分区
mkfs.fat -F32 /dev/sda1  #格式化引导分区
mkfs.ext4 /dev/sda3  #格式化主分区
mkswap /dev/sda2  #格式化swap
swapon /dev/sda2
mount /dev/sda3 /mnt
mount --mkdir /dev/sda1 /mnt/boot
crohroot
```

更换国内快速源

```bash
#备份源
cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak   
#筛选国内源
reflector --country China --age 24 --sort rate --protocol https --save /etc/pacman.d/mirrorlist 
#更新源
pacman -Syy
pacstrap /mnt linux-zen linux--zen-firmware base base-devel vim bash-complection
genfstab -U /mnt >> /mnt/etc/fstab    #生成文件系统表
arch-chroot /mnt    #进入新系统根目录
pacman -Syy    #更新一下新系统的源
```

进入安装好的系统进行配置

```bash
#更新时间
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc
vim /etc/locale.gen
locale-gen
vim /etc/locale.conf
添加：LANG=en_US.UTF-8

#更新主机名
echo "arch" >> /etc/hostname
useradd -m rain
passwd rain	
vim /etc/sudoers
rain ALL=(ALL) NOPASSWD:ALL
#安装cpu
cat /proc/cpuinfo    # 查看cpu型号
pacman -S amd-ucode    # amd 电脑安装
pacman -S intel-ucode   # intel 电脑安装
#安装grub启动程序
pacman -S grub efibootmgr efivar os-prober
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=Arch --rechechk
报错加上--removable
接下来使用 vim 编辑 /etc/default/grub 文件：
vim /etc/default/grub
进行如下修改：
去掉 GRUB_CMDLINE_LINUX_DEFAULT 一行中最后的 quiet 参数
把 loglevel 的数值从 3 改成 5。这样是为了后续如果出现系统错误，方便排错
生成grub配置文件
grub-mkconfig -o /boot/grub/grub.cfg
```

### 自动安装

```bash
archinstall
```

## 桌面环境选择

### 显示服务器

**Xorg**：对于大多数用户和桌面环境，是最安全和兼容的选择。

**Wayland**：如果你使用的是现代桌面环境（如 GNOME 或 KDE Plasma），并希望获得更好的性能和安全性。

**Mir** 和 **DirectFB** 通常在特定场景或嵌入式系统中使用，普通桌面用户较少涉及。

### 显示管理器

**SDDM**：KDE Plasma 用户推荐使用，因为它与 KDE Plasma 集成良好且易于配置。

**GDM**：GNOME 用户推荐使用，提供最佳的 GNOME 桌面体验。

**需要轻量级解决方案的用户**：推荐使用 **LightDM** 或 **LXDM**。

**最简单和轻量级需求的用户**：可以考虑 **XDM**

### 桌面环境

**GNOME**：一个功能丰富、用户友好的桌面环境，提供完整的桌面体验，包括窗口管理器、文件管理器、邮件客户端、网页浏览器等

**KDE Plasma**：一个现代化的桌面环境，以其美观和高度可定制性而闻名，提供丰富的桌面效果和应用程序

**XFCE**：一个轻量级且高效的桌面环境，适合资源有限的系统，同时提供完整的桌面功能

**LXDE**：另一个轻量级桌面环境，设计简单，资源占用少，适合老旧或低配置的计算机。

**Cinnamon**：一个提供传统桌面体验和现代化功能的桌面环境，界面直观，易于使用

**Deepin Desktop Environment (DDE)**：深度操作系统开发的桌面环境，以其美观和用户友好的界面而受到欢迎

**MATE**：GNOME 2 的一个分支，提供传统桌面体验，适合喜欢经典 GNOME 界面的用户。

**Enlighten**：Lumina 桌面环境的一部分，是一个现代化的桌面环境，设计简洁，易于使用。

**i3**：一个轻量级的窗口管理器，适合喜欢平铺式窗口管理的用户。

**Awesome**：另一个平铺式窗口管理器，高度可定制，适合高级用户。

## 安装kde桌面环境

```
sudo pacman -S plasma sddm 
```

