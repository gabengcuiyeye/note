# 使用fiddler拦截并修改https请求
### 步骤1.设置抓取https请求
在菜单栏点击tools->选择telerik fiddler options->如下图勾选https选项。然后就可以抓取https请求了。

![alt](http://km.midea.com/uploads/imgs/e5ff10201582.png)
### 步骤2.在fiddler 命令行输入bpu清除以往断点。
如下图所示：
![alt](http://km.midea.com/uploads/imgs/a7bf2afd4f9e.png)
### 步骤3.输入bpu + 想要拦截和修改的路径
如下图所示
![alt](http://km.midea.com/uploads/imgs/3398ebc75467.png)
### 步骤4.发起请求，然后页面上会出现这样的界面

![alt](http://km.midea.com/uploads/imgs/7a6a138dc19c.png)
### 步骤5.修改请求
1. 1.双击红框内的内容，这时我们可以修改请求内容了，比如双击修改category_id的值为10034，修改完成后点击run to completion，修改后的请求将被发到服务器，并返回新数据。
2. 2.点击break on response 时，返回的数据到达fiddler但是还没返回浏览器，这时再点击 run to completion,数据即可返回给浏览器。
![alt](http://km.midea.com/uploads/imgs/5c272bb30160.png)
### 步骤6.返回内容
![alt](http://km.midea.com/uploads/imgs/279cf7c48e53.png)
### 步骤7.调试完毕，清除断点
在fiddler命令行输入bpu即清除所有断点

![alt](http://km.midea.com/uploads/imgs/dda0fbd5f06e.png)
