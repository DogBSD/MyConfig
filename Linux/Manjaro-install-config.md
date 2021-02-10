> 一些安装Manjaro的配置信息，方便一下安装使用！


### 开源还是闭源驱动
> 为了性能，选择了默认闭源驱动。（以前自己用闭源驱动的性能比开源的好，玩游戏时候感觉到的，也并非准确）

### 换源
```bash
sudo pacman-mirrors -i -c China -m rank



# 不建议用Arch Linux CN的源,会影响Manjaro的稳定和安全性
sudo nano /etc/pacman.conf

[archlinuxcn]
Server = http://mirrors.163.com/archlinux-cn/$arch

# 安装密钥
sudo pacman -S archlinuxcn-keyring

```

### yay
```bash
sudo pacman -S yay
```

### 安装字体

> 如果不安装字体，终端的字符会显示过大，看着非常的不舒服

```bash
sudo pacman -S wqy-bitmapfont
sudo pacman -S wqy-zenhei
```

### Manjaro修改主目录为英文
```bash
$ sudo pacman -S xdg-user-dirs-gtk
$ export LANG=en_US
$ xdg-user-dirs-gtk-update
$ #然后会有个窗口提示语言更改，更新名称即可
$ export LANG=zh_CN.UTF-8
$ #然后重启电脑如果提示语言更改，保留旧的名称即可

# 参考：https://www.jianshu.com/p/73299b8e3f58
```

### 输入法

```bash
yay -S fcitx5-im
sudo nano ~/.pam_environment

INPUT_METHOD  DEFAULT=fcitx5
GTK_IM_MODULE DEFAULT=fcitx5
QT_IM_MODULE  DEFAULT=fcitx5
XMODIFIERS    DEFAULT=\@im=fcitx5

# 输入法引擎
yay -S fcitx5-rime
# 输入方案
yay -S rime-cloverpinyin

# 创建并写入rime-cloverpinyin的输入方案
nano ~/.local/share/fcitx5/rime/default.custom.yaml

patch:
  "menu/page_size": 8
  schema_list:
    - schema: clover

# 安装中文维基百科词库
yay -S fcitx5-pinyin-zhwiki-rime
# 配置主题（可选）
yay -S fcitx5-material-color

# 注销后重新登录打开，完成下图的配置后，点击重新启动


参考：
https://wiki.archlinux.org/index.php/Fcitx5_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)
https://zhuanlan.zhihu.com/p/114296129
```

![参考全局选项](https://pic2.zhimg.com/80/v2-abf9d3ea94a0472c2e3987d26b6be211_720w.jpg)

### zsh
```bash
# 默认manjaro安装了zsh
cat /etc/shells

chsh -s /usr/bin/zsh

# ohmyzsh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh

# 主题
ys

# 插件
zsh-autosuggestions  检索输入过的命令并匹配最相似的
zsh-syntax-highlighting  当前命令是否正确，错误红色，正确绿色

# 自带
sudo   按两下ESC，就会在命令行头部加上sudo
extract  提供一个 extract 命令，以及它的别名 x；以后 tar, gz, zip, rar 全部使用 extract 命令解压
cp 提供一个 cpv 命令，这个命令使用 rsync 实现带进度条的复制功能
colored-man-pages  给你带颜色的 man 命令

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

plugins=(git cp sudo extract colored-man-pages zsh-autosuggestions zsh-syntax-highlighting)
```
