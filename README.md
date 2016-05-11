## fork浩阳师兄的主题

后续会上传在搭建过程中遇到的一些问题。

### 遇到的问题
1. 先是通过ruby下载jekyll的资源库问题，老是出现ssl错误。
![资源](http://d.picphotos.baidu.com/album/s%3D1000%3Bq%3D90/sign=78428020f036afc30a0c3b658329d0b5/2fdda3cc7cd98d107ae4c1d1263fb80e7bec901a.jpg)

上网查找国内的资源仓库，发现都不好使用。于是加了rubyQQ群了解，得到了阿里云的库。
![aliyun](http://g.picphotos.baidu.com/album/s%3D1000%3Bq%3D90/sign=d1ce81e10d55b31998f986757399b957/8c1001e93901213fc603833c53e736d12f2e951a.jpg)
http://mirrors.aliyun.com/rubygems/ 
RubyGems简称gems，是一个用于对 Ruby组件进行打包的 Ruby 打包系统。。。RubyGems的功能类似于Linux Ubuntu下的apt-get。使用它可以方便第从远程服务器下载并安装Rails。

2. 使用jekyll s启动jekyll服务去测试的时候出错:
![](http://e.picphotos.baidu.com/album/s%3D550%3Bq%3D90%3Bc%3Dxiangce%2C100%2C100/sign=c6ba28720bf431adb8d2433c7b0ddd92/d1a20cf431adcbef0204b3e6abaf2edda3cc9f1a.jpg?referer=59f8182e9e25bc31724a35a8d9f8&x=.jpg)
查了下，jekyll安装少东西了。按照stackoverflow上大牛的提示，重新卸载安装：
![](http://e.picphotos.baidu.com/album/s%3D550%3Bq%3D90%3Bc%3Dxiangce%2C100%2C100/sign=52d05b1c7bd98d1072d40c341104c933/a2cc7cd98d1001e9450cd9efbf0e7bec54e7971a.jpg?referer=b71eb1840e23dd5478649358d1f8&x=.jpg)
![](http://f.picphotos.baidu.com/album/s%3D550%3Bq%3D90%3Bc%3Dxiangce%2C100%2C100/sign=8c93791b3edbb6fd215be523391fda25/80cb39dbb6fd52660d5ff1f4ac18972bd50736de.jpg?referer=12b5e6c78d82b90164baf70372b5&x=.jpg)

3. 最蛋疼的一个问题
一切修改部署完后，在本地进行写文章发布的时候，老是出现:
Regenerating: 1 file(s) changed at 2016-05-05 16:14:31 Liquid Exception:divided by 0 in index.html 
一直无法解决，后来issues中有人遇到同样的问题，是_posts提交文章目录下的文章数目小于3会出现的。
于是我改了，但是还是重复出现相同的错误。。找到蛋疼的问题了。。我提交的文章都是当天，比如说5.10号，文章无效，这个导致文章数目不满足或者标签数目不满足出错。
查了下：
由于jekyll 3（github目前的jekyll版本）默认对于认定为"未来"的post，是不生成的，详情可以参考Future posts - Jekyll。我把所有文件改成5.9号就可以了。
具体问题好像在feed.xml里面，具体没有研究。。真是蛋疼。

结束。我的博客地址是：[iver3on的博客](http://www.zhangwenbo.net),欢迎大家访问。

