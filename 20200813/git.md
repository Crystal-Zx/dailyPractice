## Git使用教程
> 原文出自：[Git使用教程：最详细、最傻瓜、最浅显、真正手把手教！](https://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247487262&idx=2&sn=5c2aa3be4a9422e7b778e245daf5389f&chksm=e9c5f6afdeb27fb9defa48fd7c279662c3a3b72ec787f158af270ec392275bbeb6e070b2f22c&mpshare=1&scene=23&srcid=1017gdrlB3XPLoviLBJD7wA4#rd)

### 一、Git是什么？
Git是目前世界上最先进的分布式版本控制系统
工作原理/流程：
![Git工作原理/流程](https://mmbiz.qpic.cn/mmbiz_png/e1jmIzRpwWiaEynpFwWSmr59icj386rKKxiaCC3m4XHaxHaaqLkYlukTUALnHN74icx3VZyIM3uEXz7JA9ldicwe8BQ/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)  
+ Workspace： 工作区
+ Index/Stage： 暂存区
+ Repository： 仓库区（或本地仓库）
+ Remote： 远程仓库

### 二、SVN与Git的最主要区别
<font style="color: rgb(227,79,140);">**SVN**</font> 是<font style="color: rgb(227,79,140);">**集中式版本控制系统**</font>，版本库是集中放在中央服务器的。而干活的时候，用的都是自己的电脑，所以首先要从中央服务器那里得到最新的版本，然后干活，干完活后，需要把自己做完的活推送到中央副武器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快；如果在互联网下网速又不够快，就会影响开发效率。  
<font style="color: rgb(227,79,140);">**Git**</font> 是<font style="color: rgb(227,79,140);">**分布式版本控制系统**</font>，那么它就没有中央服务器，每个人的电脑就是一个完整的版本库，工作时不需要联网。多人协作的时候，只需要将自己本地的修改推送给对方就可以了。  

### 三、Git安装
> [安装Git - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)（网站内有git教程）  
> [Windows系统Git安装教程（详解Git安装过程）](https://www.cnblogs.com/xueweisuoyong/p/11914045.html)

### 四、Git操作 ★★★
