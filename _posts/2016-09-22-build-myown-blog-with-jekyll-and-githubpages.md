---
layout: post
title: "Github Pages +Jekyll建站"
category: myexception
---

> 很早就想找个偏僻地方碎碎念，却一直没有一百块。  

日益完善的博客类产品和接踵而来的广告，或许是想督促着自己更新，找来网上的教程，一步步照做，从
[Github Pages + Jekyll 独立博客一小时快速搭建&上线指南](http://playingfingers.com/2016/03/26/build-a-blog/)、[如何搭建一个独立博客——简明 Github Pages与 jekyll 教程](http://cnfeat.com/blog/2014/05/10/how-to-build-a-blog/)学到了不少关于设置DNSpod解析域名，添加CNAME等等这些。  
教程里很详细，我就不再重复了，作为存档，记录一下途中遇到的问题。  
  
+ 购买域名后手快点了支付宝付款，需要等待一段时间（也许是明天也许是很多天）后才会显示购买成功，用信用卡或银行卡会来得快一些。  
+ 荒废了很久的github重见天日，创建ssk密钥后连接失败。  
	提示  

		Permission denied (publickey).

	解决方案：  
	
	先备份密钥

		$ ls -l
		$ mkdir key_backup 
		$ cp id_rsa* key_backup 
		$ rm id_rsa*

	再次提示  

		$ ssh -T git@github.com
		Permission denied (publickey).

	加载私钥  

		$ ssh-add -l
		$ ssh -T git@github.com

	提示“Yo've successfully authenticated, but Github does not provide shell access.”  

+ 参考[Markdown 语法说明 (简体中文版)](http://www.appinn.com/markdown/#p)进行书写  
  
+ 更换主题  
[极简灰](https://github.com/mytharcher/SimpleGray)中讲到“除非你想改进这个主题，否则请不要fork此项目作为你博客的起点，因为fork后你的所有提交和推送都会在整个network图中显示出来。所以更推荐你使用clone的方式创建自己的站点，以免给所有使用此主题的人造成干扰。”之前的fork可能给[lenage](http://blog.lenage.com)造成了困扰,极简灰打开速度很快，故更改主题一探究竟。  

+ Git问题总结  
	1.在已经配好ssh key之后，新建helloworld仓库，试图讲之前建立的README.md文件上传失败，
  报错Permission denied (publickey).  
  解决方案：将新建的空仓库clone到本地后，再次上传。  
 
	2.在上传README.md到helloworld中时，最后一步出现  
  error:src refspec master does not match any  
  分析：由于空目录不能提交上去，前一步已经将文件添加到origin中   
  解决方案：按照空目录处理，将git基本命令合集等文件一同上传  

	3.切换分支  

		$ git push origin master
		error:src refspec master does not macth any.
		error:无法推送一些引用到'https：//geithub.com/hehedanli/hehedanli.github.io'
		$ git branch
		* gh-pages
		$ git checkout -b master
		切换到一个新分支'master'
		$ git branch
		  gh-pages
		* master
		$ git push origin master

	github pages需要在master分支上。  

听说离2017年到来只剩100天了，希望能偶尔更新。  


