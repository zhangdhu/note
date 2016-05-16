zsh安装与使用.md

on-my-zsh 安装

这里只介绍一种安装方法，其它方法请到on-my-zsh进行查看。

 

1. 克隆仓库

git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
 

2. 如果你已存在~/.zshrc文件，则备份现有的~/.zshrc文件

cp ~/.zshrc ~/.zshrc.orig
 

3. 创建一个新的zsh配置文件

cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
 

4. 改变默认的Shell

chsh -s /bin/zsh
 

5. 重新启动你的终端（Terminal）

 

 

还有些很囧的情况会发现，例如是改变不了默认的Shell，导致部分人以为是安装失败，毫无头绪。其实遇到这种情况，只需要在终端输入zsh，即可完成切换，只不过默认不是zsh：

$ zsh
➜  ~ git:(master) ✗ 
是的，由于不是默认，手动切换后的格式就是这样。 

 

另外，相关的alias可以复制到~/.zshrc文件里，最后使用source更新一下文件即可：

✗ source ~/.zshrc
