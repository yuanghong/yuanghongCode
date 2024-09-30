# vue前端环境搭建

## 1.使用node.js配置VUE

### 1.1 安装node.js

从node.js官网下载 https://nodejs.org/en（建议安装16以上版本）

![1726709664776](assets/1726709664776.png)

安装 一直点击下一步就好，期间注意安装路径，npm package manager 是默认不安装的，这里要给选择安装。

### 1.2 配置npm在安装全局模块时的路径和缓存cache的路径

1.2.1 配置npm代理： 打开C:\Users\ywx1270277下的.npmrc文件，配置代理

![1726710198625](assets/1726710198625.png)

把这段话粘贴进文件并保存

registry=https://npm.cloudartifact.dgg.dragon.tools.huawei.com/artifactory/api/npm/sz-npm-public/
sass_binary_site=http://mirrors.tools.huawei.com/node-sass/
phantomjs_cdnurl=http://mirrors.tools.huawei.com/phantomjs/
chromedriver_cdnurl=http://mirrors.tools.huawei.com/chromedriver/
operadriver_cdnurl=https://mirrors.tools.huawei.com/operadriver
electron_mirror=https://mirrors.tools.huawei.com/electron/
python_mirror=https://mirrors.tools.huawei.com/python
cypress_install_binary=0
puppeteer_skip_chromium_download=0
strict-ssl=false
no_proxy=.huawei.com
cache=D:\soft\Node.js\node_cache
prefix=D:\soft\Node.js\node_global

![1726710244569](assets/1726710244569.png)

1.2.2 在node.js安装目录下新建两个文件夹 node_global和node_cache

![1726709781078](assets/1726709781078.png)

然后在cmd命令下执行如下两个命令：

npm config set prefix "D:\soft\Node.js\node_global"

npm config set cache "D:\soft\Node.js\node_cache"

### 1.2 配置环境变量

在环境变量 -> 系统变量中新建一个变量名为 “NODE_PATH”，值为D:\soft\Node.js\node_modules

![1706851723258](assets/1706851723258.png)

编辑用户变量里的Path，将相应npm的路径改为：D:\soft\Node.js\node_global，如下：

![1726709912079](assets/1726709912079.png)

![1726709884587](assets/1726709884587.png)

### 1.3 测试

执行 node -v 和 npm -v 查看版本号

![1726709973281](assets/1726709973281.png)

在管理员模式下执行 npm install webpack -g安装webpack，如下：

![1726710042426](assets/1726710042426.png)

## 2.运行项目文件

1.打开webservice项目，在terminal执行npm install安装依赖

![1726710745725](assets/1726710745725.png)

2.执行npm run build，出现以下界面证明项目运行成功

![1726710831049](assets/1726710831049.png)

## 2 配置Vue项目（无需执行）

### 2.1安装Vue脚手架

Vue脚手架是Vue官方提供的标准化开发工具

中文官方文档  https://cli.vuejs.org/zh/

具体安装步骤（在cmd下执行）

第一步（仅第一次执行）：全局安装@vue/cli

  npm install -g @vue/cli

第二步：切换到你要创建项目的目录，然后使用命令创建项目

vue create ****

![1702725413996](C:\Users\YWX127~1\AppData\Local\Temp\1702725413996.png)

这里会提示你创建vue2.0还是3.0项目，根据需要选择即可，配置完成后出现下图所示的界面

![1702725858471](C:\Users\YWX127~1\AppData\Local\Temp\1702725858471.png)

第三步：启动项目

依次执行命令，项目启动成功如下图所示

cd 项目目录

npm run serve

![1702725953175](C:\Users\YWX127~1\AppData\Local\Temp\1702725953175.png)

### 2.2测试

用浏览器打开http://localhost:8080/或者http://10.143.45.48:8080/，出现下图说明Vue项目启动成功

![1702726059305](C:\Users\YWX127~1\AppData\Local\Temp\1702726059305.png)

## 3 安装Vue开发者工具（无需执行）

一、Chrome浏览器安装方式：
①：点击右上角三个点
②：点击更多工具
③：点击扩展程序
④：点击右上角的开发者模式，将他启用
⑤：将下载的Vue.crx文件直接拖动到浏览器窗口即可

!1702726275539](C:\Users\YWX127~1\AppData\Local\Temp\1702726275539.png)

二：Edge浏览器安装方式
①：点击浏览器右上角的三个点
②：点击扩展
③：点击左下角的开发人员模式，将他启用
④：将Vue.crx文件拖动到浏览器即可

![1702726286437](C:\Users\YWX127~1\AppData\Local\Temp\1702726286437.png)

安装成功后，浏览器右上方的Vue开发者工具图标将被点亮

![1702726392609](C:\Users\YWX127~1\AppData\Local\Temp\1702726392609.png)





