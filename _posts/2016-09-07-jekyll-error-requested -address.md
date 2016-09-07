---
layout: post
title: "jekyll 3.0.1 | Error:  Cannot assign requested address - bind(2) for "
category: myexception
---
> 运行jekyll server，报错——  
jekyll 3.0.1 | Error:  Cannot assign requested address - bind(2)  


修改主题为自己的站点时，参考极简灰作者的说明，无法运行jekyll预览的情况下，push了文件，留到今天来修改。  
参考[jekyll配置说明](http://jekyllcn.com/docs/configuration/)  服务器选项
  
	detach:  false
	port:    4000 
	host:    127.0.0.1
	baseurl: "" # does not include hostname
  
修改时将_config.yml文件中的变量host修改为站点域名，产生冲突（或许是我哪里没设置对？）。  
  
解决方案：将_config.yml文件中的host: stillnoon.com修改为url: stillnoon.com  

PS:markdown语法中，代码行和前后要有空行

