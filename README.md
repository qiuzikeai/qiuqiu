安装与依赖
Tampermonkey安装与使用
进入官网tampermonkey（官网中有详细使用教程）,选择对应的浏览器版本
 
随后点击下载，完成安装。如果使用的是Chrome，可以在应用商店搜索Tampermonkey并添加为扩展程序即可。
安装完成后，在浏览器右上角扩展处会出现tampermonkey的标志。

将鼠标移到该标志处即可查看功能，如图8所示。点进管理面板即可进入tampermonkey页面。
 
Nodejs安装与环境配置
1. 安装包下载：点击官网下载页nodejs下载，根据自己电脑系统及位数选择版本。
2.	完成安装后需配置环境变量，具体配置方法可参考nodejs安装与环境变量配置。
3.	在CMD窗口中执行命令node -v即可查看node是否安装成功极其版本。

Websocket依赖环境配置
在CMD中执行命令npm i ws配置Websocket，若出现错误，则以管理员模式打开CMD重新执行。

服务器部署
使用自己的云服务器，将server.js以及watchmoviestogether.js放到云服务器同一目录下，开放server.js中对应端口的TCP连接防火墙。
操作逻辑与最终实现效果
首先将watchmoviestogether.js中的内容部署到tampermonkey中，使用ssh连接到云服务器（或其他方式），在server.js所在目录中执行命令node server.js开启监听，如果无法实现监听，表明需要证书，则访问https://yourURL:yourPort   获取浏览器信任自签名CA证书即可，若还是无法实现，则需要额外配置证书。

打开适配的网页播放器，本次测试是在Edge浏览器中使用哔哩哔哩网页播放器https://www.bilibili.com， 点进去后在右上角扩展栏tampermonkey标志中打开watchmoviestogether脚本，可以看到页面中出现了watchmoviestogether的按钮
 
点击该按钮，即可进入到初始版面

对于房主端，输入自己的昵称，点击创建即可创建房间并自动生成房间ID，如图15所示。

对于其他成员，输入自己的昵称，并输入对应的房间ID，即可实现加入对应的房间。
  
随后房主端即可控制视频的播放，其他用户可实现同步观看。效果如下面视频所示：双击即可进入并播放视频
 
使用Tips

对房主端
1.	当目前所在页面为页面A并且脚本保存连接，如果此时打开一个新的页面B，打开方式无论是从A页面中点击新的链接打开还是直接单独打开新的窗口进行搜索，甚至是在其他页面进行刷新，都会使连接转换到新的页面B，旧的页面A的连接会自动关闭。简单来讲就是如果有保存连接的A页面之外的新页面打开，连接就会自动转移。
2.	如果直接关闭了页面A，在5s内打开或者刷新其他页面，都会使连接转移到此此新的页面中，如果超过5s，websocket连接会自动失效。
3.	当房主端打开了一个新的页面但是此页面没有视频播放，成员端是不会同步更新的，只有当房主端播放了某个视频，成员端才会同步更新。
   
对成员端
1.	如果房主在选择视频时，即没有进入到播放界面，成员端是不会自动同步的，一旦房主进入了某个视频的播放，成员就会自动同步房主对视频的暂停、播放、倍速调整、切换视频等操作。
2.	成员端对视频的操作不会同步给房主，成员端在打开新的页面时也不会把连接从正在播放的页面专业过来，甚至成员端操作的时候有可能导致连接失效，因此不建议成员端对视频进行操作。
3.	成员端只有在房主切换视频后自动跳转页面时连接会走到转移，自动转移可以跨网站进行，比如从哔哩哔哩播放器转移到优酷播放器。

