# FIS2探索集结 #
>

>  前提：1.本人有幸参与百度作业帮开发者团队进行实习，接触学习了fis2前端自动化工具，在此做出总结性文档，相关详细内容请参照：fis.baidu.com进行文档参照，作者在此进行简单化解读。
> 

>  2.本人电脑系统环境为windows 7，fis框架对于路径概念接触很多，在此建议先屡清楚相对路径与绝对路径，本地与服务器路径的一系列概念。
## FIS2安装 ##
> FIS使用Node.js开发，以npm包的形式进行发布，首先需要安装node.js,首先进入官网进行下载：地址：http：//www.nodejs.org/download/,下载之后进行安装即可，默认安装路径是c:\program FILES\nodejs路径下面


> **安装完毕后，打开命令窗（cmd)，输入如下代码**
> 
> 
    node -v；
    npm -v



> **安装fis2**
> 装好node和npm之后，在命令行中输入：
    npm install -g fis




> **安装java jre环境**


> 网址：java.com


> 安装java，下载，安装即可。


> **安装php-cgi环境**


> 1.首先下载安装好XAMPP，安装好相应的php和apache环境

> 2.安装完毕后，打开XAMPP目录下php/ext文件，查看有无php.ini文件，有的话即可进行下一步，将php添加至计算机环境变量path下


>  3.安装完毕后，命令行输入：
    php-cgi -v

> **查看FIS本地调试服务器**


>  打开命令行，输入：
    fis server start
> 

> 出现如下图则调试服务器安装成功，同时系统默认浏览器会以80端口打开一个网页，以后本地开发的项目都将通过此服务器进行调试。
 ## FIS2 发布项目操作及调试
***发布你本地项目demo***
>

>  首先，打开命令行，进入你的本地项目文件路径：（我以自己的项目来进行示例）
> 
> 我的发布示例如下：
    

> cd fis2-demo；//进入本地自己项目文件
    
> fis-install;//安装可能用的jquery项目组件
> fis release；//发布项目
> fis server start；//将项目发布至调试服务器上即可实现页面效果展示


> 注意：
>

>  1.在第二步进行发布项目时，自己项目中的css，js引入文件路径加上“../",因为此处本地demo是相对路径，而这一步是将你的项目文件从本地发布到服务器中所在项目文件，所以路径应该引入绝对路径，否则样式与脚本将会无效。
>  
> 2.在通过fis server start 将项目发布到本地的调试服务器上时，这里可能会出现端口错误，此处只需要通过 fis server start -p [端口号】指定新端口即可。
 
> 3.fis server start open将会让你打开服务器所在文件夹www，此处切记，如果你将自己的项目文件复制粘贴放置于服务器文件目录下，也可以实现访问，但这里只是通过本地文件路径访问，不是fis的宗旨所在（用过wamp的同学喜欢这错误）
> 

> **发布调试线上项目**
> 
> 此处原理与文档给的案例相同，总的示例我将不给出代码，只给出实现具体思路。
> 
> 1.打开GIT bash输入git clone将项目从git远程库clone下来（也可以通过git GUI来实现）
> 

> 2.进入你的项目文件，在项目文件路径下继续执行与你发布本地项目代码一致的操作。
> ## FIS2资源压缩与合并 ##
> 
> 资源压缩与合并可以减少http请求可以优化前端页面，进入你的项目路径
输入以下指令：
>

>  `fis release --optimize`或者`fis release -o`即可实现压缩资源。
> 

> 输入`fis release -d <path/output>`指定你文件的输出目录。
> 

> **资源合并**
> 
> 编辑器打开fis-conf.js文件，加入pack配置（fis通过pack进行资源文件合并）
> `fis.config.set('pack', {
    '/pkg/lib.js': [
        'js/lib/jquery.js',
        'js/lib/underscore.js',
        'js/lib/backbone.js',
        'js/lib/backbone.localStorage.js',
    ]
});`
> 打开cmd，通过npm包管理工具进行插件安装：
> 

> `npm install -g fis-postpackager-simple`
> 插件安装完毕后，进入项目根目录下fis-conf.js进行配置
> 

> cd fis-quickstart-demo


> vi fis-conf.js #vi是linux下的文本编辑器，windows用户可以选用任意文本编辑器对fis-conf.js文件进行编辑。


> //file : fis-conf.js


> fis.config.set('modules.postpackager', 'simple');
> 为了开发调试时更加方便 fis release 默认不会合并资源，在指定了 --pack 参数后，FIS才会进行打包合并处理。

fis release --optimize --md5 --pack # fis release -omp
> **自动打包**
> 
> 利用simple插件，我们还可以按页面进行自动合并，将没有通过pack设置打包的零散资源自动合并起来。



> //file : fis-conf.js


> //开启autoCombine可以将零散资源进行自动打包


> fis.config.set('settings.postpackager.simple.autoCombine', true);


> 再次运行FIS构建项目



> fis release -omp


> 我们会发现剩余的零散资源已经被自动合并了。
> 到这里可以掌握大部分开发fis2功能了,可以尝试开发了