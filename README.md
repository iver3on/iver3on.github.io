### [fork自Gaohaoyang](https://github.com/Gaohaoyang/gaohaoyang.github.io)

后续会上传在搭建过程中遇到的一些问题。

### 遇到的问题

1. 先是通过ruby下载jekyll的资源库问题，老是出现ssl错误。
  ![资源](https://raw.githubusercontent.com/iver3on/blogPic/master/QQ%E6%88%AA%E5%9B%BE20160509195427.jpg)

  上网查找国内的资源仓库，发现都不好使用。于是加了rubyQQ群了解，得到了阿里云的库。

  ![aliyun](https://raw.githubusercontent.com/iver3on/blogPic/master/QQ%E6%88%AA%E5%9B%BE20160509195445.jpg)
  http://mirrors.aliyun.com/rubygems/ 

  RubyGems简称gems，是一个用于对 Ruby组件进行打包的 Ruby 打包系统。。。RubyGems的功能类似于Linux

  Ubuntu下的apt-get。使用它可以方便第从远程服务器下载并安装Rails。

2. 使用jekyll s启动jekyll服务去测试的时候出错:

  ![x](https://raw.githubusercontent.com/iver3on/blogPic/master/QQ%E6%88%AA%E5%9B%BE20160509194043.jpg)

  查了下，jekyll安装少东西了。按照stackoverflow上大牛的提示，重新卸载安装：

  ![y](https://raw.githubusercontent.com/iver3on/blogPic/master/QQ%E6%88%AA%E5%9B%BE20160509195401.jpg)

3. 最蛋疼的一个问题
  一切修改部署完后，在本地进行写文章发布的时候，老是出现:
  Regenerating: 1 file(s) changed at 2016-05-05 16:14:31 Liquid Exception:divided by 0 in index.html 

  一直无法解决，后来issues中有人遇到同样的问题，是_posts提交文章目录下的文章数目小于3会出现的。 
  
  于是我改了，但是还是重复出现相同的错误。。找到蛋疼的问题了。。我提交的文章都是当天，比如说5.10号，文章无效，这个导致文章数目不满足或者标签数目不满足出错。
  查了下：
  
  由于jekyll 3（github目前的jekyll版本）默认对于认定为"未来"的post，是不生成的，详情可以参考Future posts - Jekyll。我把所有文件改成5.9号就可以了。 
  
  具体问题好像在feed.xml里面，具体没有研究。。真是蛋疼。 
  
  结束。我的博客地址是：[iver3on的博客](http://www.zhangwenbo.net),欢迎大家访问。 
  
  branch Test

