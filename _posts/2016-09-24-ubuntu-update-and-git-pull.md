---
layout: post
title: "ubuntu安装更新报错 & git pull"
category: myexception
---

### ubuntu安装更新报错资源被锁

> 从设置中安装更新，进度条始终卡在一半，下载内容的“详细”页面莫名其妙变成了空白，非常不信任自家网络的我，试图从终端看看`````由于不可抗力dl.google.com被我们纯洁的友谊净化了。  
恍惚间又冒出了别的错误。  

执行  

		$ sudo apt update && sudo apt upgrade

后提示  

		正在读取软件包列表... 完成
		E: 无法获得锁 /var/lib/apt/lists/lock - open (11: 资源暂时不可用)
		E: 无法对目录 /var/lib/apt/lists/ 加锁

参考[Ubuntu使用教程：E: 无法获得锁 /var/lib/apt/lists/lock - open (11 资源临时不可用)](http://www.linuxidc.com/Linux/2014-06/103437.htm)解决。  

方法一：  
输入命令  

		sudo dpkg --configure -a

方法二：  
出现这个问题的原因可能是有另外一个程序正在运行，导致资源被锁不可用。而导致资源被锁的原因，可能是上次安装时没正常完成。在大部分情况下，问题的原因在于其它的程序如系统的自动更新、新立得等正在使用apt-get进程，所以解决方法也就是将这一进程关闭。  
输入命令（亲测可用）  

		sudo rm /var/lib/apt/lists/lock

或  
 
		sudo rm /var/cache/apt/archives/lock
		sudo rm /var/lib/dpkg/lock
 
再安装想装的包，即可解决。  
 
方法三：  
首先在终端输入“ps -aux”查看是否有使用apt-get的程序,,找到使用apt-get的程序,查看其PID号,然后输入sudo kill PID 杀死该进程。  

### 推送文章git push origin master报错  

		error: 无法推送一些引用到 'https://github.com/hehedanli/hehedanli.github.io.git'
		提示：更新被拒绝，因为远程仓库包含您本地尚不存在的提交。这通常是因为另外
		提示：一个仓库已向该引用进行了推送。再次推送前，您可能需要先整合远程变更
		提示：（如 'git pull ...'）。
		提示：详见 'git push --help' 中的 'Note about fast-forwards' 小节。

根据提示，执行git pull命令，来查看冲突内容，有的时候，它会自动合并，有的时候需要手动来解决冲突（按照提示来就可以了）

+ 总结

    首先git push origin branch-name推送自己的修改；  
    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；  
    如果合并有冲突，则解决冲突，并在本地提交；  
    没有冲突或者解决掉冲突后，再用git push origin branch-name推送。  



