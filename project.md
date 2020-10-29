##  配置composer 国内加速镜像
    '''
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
    '''
    
##  创建laravel框架项目
    '''
    cd ~/Code
    composer create-project laravel/laravel Laravel --prefer-dist "7.*"
    '''
## 第一行Laravel 代码
    修改 resources/views/welcome.blade.php 文件，加入个人信息
    '''
        <!DOCTYPE html>
        <html>
            <head>
                <title>Laravel</title>
                <style>
                    html, body {
                        height: 100%;
                    }
        
                    body {
                        margin: 0;
                        padding: 0;
                        width: 100%;
                        display: table;
                        font-weight: 100;
                        font-family: "Helvetica Neue", NotoSansHans-Regular,AvenirNext-Regular,arial,Hiragino Sans GB,"Microsoft Yahei","Hiragino Sans GB","WenQuanYi Micro Hei",sans-serif;
                        color:#777;
                    }
        
                    .container {
                        text-align: center;
                        display: table-cell;
                        vertical-align: middle;
                    }
        
                    .content {
                        text-align: center;
                        display: inline-block;
                    }
        
                    .title {
                        font-size: 66px;
                    }
                </style>
            </head>
            <body>
                <div class="container">
                    <div class="content">
                        <div class="title">Hello Laravel! - by Summer</div>
                    </div>
                </div>
            </body>
        </html>
    '''
##  Git 和 github  的常规操作    
####    1.git 用户名和邮箱的设置，--global 代表对git 进行全局设置
    、、、
        $ git config --global user.name "Your Name"
        $ git config --global user.email your@example.com
    、、、
    
####    2.设置 Git 推送分支时相关配置：
    、、、
       git config --global push.default simple
    、、、
####    3.对 Git 进行初始化：
    、、、
        cd ~/Code/Laravel
        git init
    、、、
    
####    4.将项目所有文件纳入到 Git 中
    、、、
    git add -A
    、、、

####    5.检查git 状态(输出存放在 Git 暂存区的文件)
    、、、
    git status
    、、、
    
####    6.保留改动并提交
    、、、
    git commit -m "Initial commit"
    、、、
    
####    7.查看历史提交记录：
    、、、
    git log
    commit 4d8896a697674861adec7e2ba8b7804412c0678d
    Author: Summer <summer@learnku.com>
    Date:   Wed Sep 7 07:54:11 2016 +0800
    
        Initial commit
    、、、

####    8.删除文件恢复
    、、、
    git checkout -f 
    、、、
####    9.git   分支处理
    1）创建分支
        、、、
        git checkout -d static-pages
        、、、
    
    2)切换分支
        、、、
        git checkout master 
        、、、
        
    3)合并分支
        、、、
        git merge   fake-branch
        、、、
        
    4)删除分支
        、、、
        git branch -d fake-branch
        、、、
#### 10. github  常规设置 
    1)Mac系统下查看和生成SSH Key----查看本地是否存在SSH-Key
    如果 　　# id_rsa        id_rsa.pub 存在，则执行第三步骤
    
    
    、、、
    ls -al ~/.ssh
    、、、
    
    
    2)如果没有，生成新的SSH Key，your_email：这里填写你在GitLab或者GitHub注册时的邮箱。后面的提示直接敲回车，一路完成。
    、、、
    　　#ssh-keygen -t rsa -C"you_email"
    、、、
    
    3)复制生成好的SSH Key 添加到 GitLab 或者GitHub中的SSH Key中即可。
    
    
    4)项目创建完成之后，使用以下命令将代码上传到 GitHub 上
    、、、
        cd ~/Code/Laravel
        git remote add origin git@github.com:your_username/hello_laravel.git
        git push -u origin master
    、、、
    
    
### 构建页面
    
####    1.创建应用    weibo
    、、、
    cd ~/Code
    composer create-project laravel/laravel weibo --prefer-dist "7.*"
    、、、
    
####    2.Git 来新建一个 static-pages 分支
   
    、、、
    git checkout master             // git checkout master 代表将当前分支切换到 master 分支上，
    git checkout -b static-pages    //git checkout -b static-pages 将会为你创建一个名为 static-pages 的新分支
    、、、
    
####    3.删除无用视图
    、、、
    rm resources/views/welcome.blade.php
    、、、
    
####    4.添加路由
    路径：routes/web.php
    、、、
    <?php
    
    Route::get('/', 'StaticPagesController@home');
    Route::get('/help', 'StaticPagesController@help');
    Route::get('/about', 'StaticPagesController@about');
    、、、

####    5.Laravel 中我们较为常用的几个基本的 HTTP 操作
    GET 常用于页面读取
    POST 常用于数据提交
    PATCH 常用于数据更新
    DELETE 常用于数据删除
    
####    6.生成静态页面控制器    
    、、、
    php artisan make:controller StaticPagesController
    、、、
    
    app/Http/Controllers/StaticPagesController.php 默认代码
    、、、
    
        <?php
        
        namespace App\Http\Controllers;
        
        use Illuminate\Http\Request;
        
        class StaticPagesController extends Controller
        {
            //
        }

    、、、
####    7.为控制器加上这三个动作来处理从路由发过来的请求：
    、、、
        <?php
        
        namespace App\Http\Controllers;
        
        use Illuminate\Http\Request;
        
        class StaticPagesController extends Controller
        {
            public function home()
            {
                return '主页';
            }
        
            public function help()
            {
                return '帮助页';
            }
        
            public function about()
            {
                return '关于页';
            }
        }
    、、、
    
####    8.添加静态页面视图
    、、、
    <?php
    
    namespace App\Http\Controllers;
    
    use Illuminate\Http\Request;
    
    class StaticPagesController extends Controller
    {
        public function home()
        {
            return view('static_pages/home');
        }
    
        public function help()
        {
            return view('static_pages/help');
        }
    
        public function about()
        {
            return view('static_pages/about');
        }
    }
    、、、
    
####    9.创建静态页面并配置具体页面内容
    主页：resources/views/static_pages/home.blade.php
    、、、
        <!DOCTYPE html>
        <html>
        <head>
          <title>Weibo App</title>
        </head>
        <body>
          <h1>主页</h1>
        </body>
        </html>
    、、、
    
    
    帮主页：resources/views/static_pages/help.blade.php
    、、、
        <!DOCTYPE html>
        <html>
        <head>
          <title>Weibo App</title>
        </head>
        <body>
          <h1>帮助页</h1>
        </body>
        </html>
    、、、
    
    
    
    关于页：resources/views/static_pages/about.blade.php
    、、、
        <!DOCTYPE html>
        <html>
        <head>
          <title>Weibo App</title>
        </head>
        <body>
          <h1>关于页</h1>
        </body>
        </html>
    、、、
    
####    10.使用通用视图
    配置通用视图：resources/views/layouts/default.blade.php
    
    @yield('content') 用于站位，显示内容区域 
    、、、
        <!DOCTYPE html>
        <html>
          <head>
            <title>Weibo App</title>
          </head>
          <body>
            @yield('content')
          </body>
        </html>
    、、、
    
####    11.配置模版继承   @extiends('layout.default')
    
    resources/views/static_pages/home.blade.php
    、、、
        @extends('layouts.default')
        @section('content')
          <h1>主页</h1>
        @stop
    、、、
    
    
    在 Laravel 对 home.blade.php 文件进行编译后，结果如下：
    、、、
        <!DOCTYPE html>
        <html>
          <head>
            <title>Weibo App</title>
          </head>
          <body>
            <h1>主页</h1>
          </body>
        </html>
    、、、
    
    配置其他两个页面
    resources/views/static_pages/help.blade.php
    、、、
        @extends('layouts.default')
        @section('content')
          <h1>帮助页</h1>
        @stop
    、、、
    
    
    resources/views/static_pages/about.blade.php
    、、、
        @extends('layouts.default')
        @section('content')
          <h1>关于页</h1>
        @stop
    、、、
    
####    12.修改网站标题  
    
    1.@yield 传了两个参数，第一个参数是该区块的变量名称，第二个参数是默认值
    、、、
        <title>@yield('title', 'Weibo App')</title>
    、、、
    
    
    //修改默认视图文件
    resources/views/layouts/default.blade.php：
    、、、
        <!DOCTYPE html>
        <html>
          <head>
            <title>@yield('title', 'Weibo App')</title>
          </head>
          <body>
            @yield('content')
          </body>
        </html>
    、、、
    
    //修改帮主页和关于页面标题
    
    resources/views/static_pages/help.blade.php
    、、、
        @extends('layouts.default')
        @section('title', '帮助')
        
        @section('content')
          <h1>帮助页</h1>
        @stop
    、、、
    
    resources/views/static_pages/about.blade.php
    、、、
        @extends('layouts.default')
        @section('title', '关于')
        
        @section('content')
          <h1>关于页</h1>
        @stop
    、、、
    
    
    //@yield 区块后面进行内容拼接
    resources/views/layouts/default.blade.php
    、、、
        <!DOCTYPE html>
        <html>
          <head>
            <title>@yield('title', 'Weibo App') - Laravel 新手入门教程</title>
          </head>
          <body>
            @yield('content')
          </body>
        </html>
    、、、
    
    
#### 13.Git 提交代码，构建页面结束
    、、、
        git add -A
        git commit -m "基础页面"
    、、、


##  第四章 页面优化部分

#### 切换分支，创建新的分支
    、、、
        git checkout master
        git checkout -b filling-layout-style    
    、、、

####    Laravel 项目中使用 Bootstrap 前端框架
    //composer require 是用来安装扩展包使用的命令
    
    、、、
    composer require laravel/ui:^2.0 --dev
    、、、
    
    //引入bootstrap
    、、、
    php artisan ui bootstrap 
    、、、
####    composer    安装扩展包命令
      compser require + 包名 --dev
      --dev  是指定此扩展包只在开发环境中使用
      
    、、、
    composer require laravel/ui:^2.0 --dev
    、、、

####    laravel 引入bootstrap
    '''
    php artisan ui bootstrap 
    '''

####    nvm node  npm 之间的区别

        nvm：nodejs 版本管理工具。
        也就是说：一个 nvm 可以管理很多 node 版本和 npm 版本。
        nodejs：在项目开发时的所需要的代码库
        npm：nodejs 包管理工具。
        在安装的 nodejs 的时候，npm 也会跟着一起安装，它是包管理工具。
        npm 管理 nodejs 中的第三方插件

####    nvm、nodejs、npm的关系：

        nvm 管理 nodejs 和 npm 的版本。npm 可以管理 nodejs 的第三方插件。


####    安装 nvm
    一、解决GitHub的raw.githubusercontent.com无法连接问题?
        
        1)在https://site.ip138.com/raw.Githubusercontent.com/ 
        2)输入raw.githubusercontent.com，查询IP地址     
        
        3)修改hosts Ubuntu，CentOS及macOS直接在终端输入 
          
        、、、
            sudo vi /etc/hosts    
        、、、
        
        4)添加以下内容保存即可 （IP地址查询后相应修改，可以ping不同IP的延时 选择最佳IP地址）
        
        、、、
         # GitHub Start
            52.74.223.119 github.com
            192.30.253.119 gist.github.com
            54.169.195.247 api.github.com
            185.199.111.153 assets-cdn.github.com
            151.101.76.133 raw.githubusercontent.com
            151.101.108.133 user-images.githubusercontent.com
            151.101.76.133 gist.githubusercontent.com   //中国香港
            151.101.76.133 cloud.githubusercontent.com
            151.101.76.133 camo.githubusercontent.com
            151.101.76.133 avatars0.githubusercontent.com
            151.101.76.133 avatars1.githubusercontent.com
            151.101.76.133 avatars2.githubusercontent.com
            151.101.76.133 avatars3.githubusercontent.com
            151.101.76.133 avatars4.githubusercontent.com
            151.101.76.133 avatars5.githubusercontent.com
            151.101.76.133 avatars6.githubusercontent.com
            151.101.76.133 avatars7.githubusercontent.com
            151.101.76.133 avatars8.githubusercontent.com
        #GitHub End
        、、、
    二、安装    nvm
        mac:        
        、、、
            curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
        、、、
        
        or linux     
        、、、    
            wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash    
        、、、
    
        1)注意后面的“v0.33.8”这是nvm的版本号，当前最新版本是v0.33.8 详见：https://github.com/creationix/nvm/blob/master/README.md


        2)安装完成后关闭终端，重新打开终端输入 nvm 验证一下是否安装成功，当出现“Node Version Manager”时，说明已安装成功。
        3)如果在新的终端输入 nvm 时提示：command not found: nvm，有可能是以下原因之一：    
            你的系统可能缺少一个 .bash_profile 文件，你可以创建一个此文件（可通过vi或vim命令），
            打开复制粘贴以下代码（安装nvm成功后终端的最好3行代码）进去，保存，然后再次运行
            安装命令；
            、、、
            
            export NVM_DIR="$HOME/.nvm"
            [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
            [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
                
            、、、
        4)如果上面没有解决问题，打开你的 .bash_profile 文件，并添加以下代码：
            、、、    
            source ~/.bashrc            
            、、、        
    三、mvm   常用的命令
    
        nvm install stable ## 安装最新稳定版 node，当前是node v15.1.0 (npm v6.14.8)

        nvm install <version> ## 安装指定版本，可模糊安装，如：安装v4.4.0，既可nvm install v4.4.0，又可nvm install 4.4
        
        nvm uninstall <version> ## 删除已安装的指定版本，语法与install类似
        
        nvm use <version> ## 切换使用指定的版本node
        
        nvm ls ## 列出所有安装的版本
        
        nvm ls-remote ## 列出所有远程服务器的版本（官方node version list）
        
        nvm current ## 显示当前的版本
        
        nvm alias <name> <version> ## 给不同的版本号添加别名
        
        nvm unalias <name> ## 删除已定义的别名
        
        nvm reinstall-packages <version> ## 在当前版本 node 环境下，重新全局安装指定版本号的 npm 包
    
        nvm ls  查看本机安装的 node版本    
    
    
    四、通过nvm 安装npm(mac os x64)    
        、、、
        nvm install v12.19.0   
        、、、

####   安装 yarn
    、、、
    npm install -g yarn v1.22.10
    、、、        

####    NPM 扩展包，我们重点看以下几个
    bootstrap —— Bootstrap NPM 扩展包；
    jquery —— jQuery NPM 扩展包；
    laravel-mix —— 由 Laravel 官方提供的静态资源管理工具
    。
####    设置安装器来使用国内的淘宝镜像加速
    、、、
    npm config set registry=https://registry.npm.taobao.org
    yarn config set registry 'https://registry.npm.taobao.org'
    、、、

####    yarn 安装扩展包
    、、、
     yarn install --no-bin-links
     yarn add cross-env
    、、、

####    编辑  resources/sass/app.scss 文件
    安装完成之后，让我们对 Laravel 默认生成的 app.scss 文件进行编辑，
    删除此文件里的所有内容，只留下面一行，导入 Bootstrap
    、、、
    // Bootstrap
    @import '~bootstrap/scss/bootstrap';
    、、、
####    引入saas
    Sass（一种 CSS 开发工具）专属的文件格式,
    将 Bootstrap 导入成功之后，我们需要使用以下命令来将 .scss 文件编译为 .css
    //手动编译 saas 命令
    、、、
    npm run dev
    、、、
    
    
    //自动检测编译 sass命令（一直在终端打开此窗口），在每次检测到 .scss 文件发生更改时，自动将其编译为 .css 文件：
    、、、
    npm run watch-poll
    、、、


####    优化页面
    优化默认模版，引入bootsrap
    resources/views/layouts/default.blade.php
    、、、
        <!DOCTYPE html>
        <html>
          <head>
            <title>@yield('title', 'Weibo App') - Laravel 入门教程</title>
            <link rel="stylesheet" href="/css/app.css">
          </head>
          <body>
        
            <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
              <div class="container">
                <a class="navbar-brand" href="/">Weibo App</a>
                <ul class="navbar-nav justify-content-end">
                  <li class="nav-item"><a class="nav-link" href="/help">帮助</a></li>
                  <li class="nav-item" ><a class="nav-link" href="#">登录</a></li>
                </ul>
              </div>
            </nav>
        
            <div class="container">
              @yield('content')
            </div>
          </body>
        </html>
    、、、
    
    bootstrap 默认定义的页面标签：navbar container
    resources/views/static_pages/home.blade.php
    、、、
        @extends('layouts.default')

        @section('content')
          <div class="jumbotron">
            <h1>Hello Laravel</h1>
            <p class="lead">
              你现在所看到的是 <a href="https://learnku.com/courses/laravel-essential-training">Laravel 入门教程</a> 的示例项目主页。
            </p>
            <p>
              一切，将从这里开始。
            </p>
            <p>
              <a class="btn btn-lg btn-success" href="#" role="button">现在注册</a>
            </p>
          </div>
        @stop
    、、、
    
    
    css 调整
    resources/sass/app.scss
    、、、
        // Bootstrap
        @import '~bootstrap/scss/bootstrap';
        
        body {
            font-size: 14px;
            font-weight: normal;
        }
        
        nav.navbar.navbar-expand-lg {
            margin-bot @import '~bootstrap/scss/bootstrap';
        
        body {
            font-size: 14px;
            font-weight: normal;
        }
        
        nav.navbar.navbar-expand-lg {
            margin-bottom: 20px;
        }tom: 20px;
        }
    、、、
    
    //因为我们在上面运行着 npm run watch-poll 命令，watch-poll 任务会监控着 resources 下的文件变更。
    当你保存 app.scss 的动作被 watch-poll 命令捕捉到以后，就会触发自动编译功能，将 .scss 文件编译为 .css 文件，
    并存放到 public/css 文件夹里。刷新

####    Git 代码版本控制
    、、、
    git add -A
    git commit -m "初始化样式"
    、、、


####    前端工作流梳理
     Laravel 是如何利用 Sass, NPM, Yarn, Laravel Mix 来构成一套完整的前端工作流

####    SASS 语法基础
    Sass 是一种可用于编写 CSS 的语言，起初由 Hampton Catlin 进行设计并由 Natalie Weizenbaum 开发。
    借助 Sass 我们可以少写很多 CSS 代码，并使样式代码的编写更加灵活多变。接下来我们将对 Sass 的几个主要功能进行讲解。

    1.样式文件的导入
        Sass 使用 @import 来导入其它的样式文件
        、、、
        @import '~bootstrap/scss/bootstrap';        
        、、、
        //单独一个文件进行导入：
        、、、
            @import "node_modules/bootstrap/scss/_alert.scss";        
        、、、
    
        
    2. 变量        
        Sass 还允许你在代码中加入变量，所有的变量均以 $ 开头。
        、、、
            $navbar-color: #3c3e42;
            .navbar-inverse {
              background-color: $navbar-color;
            }        
        、、、  
    
    3. 嵌套      
        Sass 还允许你在选择器中进行相互嵌套，以减少代码量。
        '''
        body div {
          color: red;
        }
        
        body h1 {
          margin-top: 10px;
        }        
        '''
        
        可写成： 
               
        、、、
        body {
          div {
            color: red;
          }
        
          h1 {
            margin-top: 10px;
          }
        }        
        、、、    
    
    4. 引用父选择器
        你还可以在 Sass 嵌套中使用 & 对父选择器进行引用：
        、、、
        a {
          color: white;
        }
        
        a:hover {
          color: blue;
        }        
        、、、
    
        可改写为：        
        
        、、、
        a {
              color: white;
              &:hover {
                color: blue;
              }
            }        
        、、、

####    NPM, Yarn, Laravel Mix  功能介绍
    1. NPM#        
        NPM 是 Node.js 的包管理和任务管理工具，其强大的功能也是 Node.js 能够如此成功的因素之一。
        在使用 NPM 安装第三方模块（也可理解为扩展包）时，你需要在 package.json 中对要安装的模块
        指定好名称和版本号。然后运行下面命令进行安装：
        
        、、、
        npm install        
        、、、
        在开始安装之前，npm install 命令会先检查 node_modules 文件夹是否已存在要安装的模块，
        如果该模块已安装，则跳过，接着安装下一模块。安装完成后，所有的第三方模块都将被下载到 node_modules 文件夹中

        1)npm 强制安装所有模块命令            
        、、、
        npm install -f        
        、、、
        
        2)NPM 和 Yarn 安装镜像加速设置：
        、、、
        npm config set registry=https://registry.npm.taobao.org
        yarn config set registry 'https://registry.npm.taobao.org'         
        、、、
        
        3)NPM 的任务管理命令：        
        、、、
        npm run watch-poll        
        、、、
    
    2. Yarn#
        Yarn 是 Facebook 在 2016 年 10 月开源的一个新的包管理器，用于替代现有的 NPM 客户端或者其他兼容 NPM 仓库的包管理工具。
        Yarn 在保留 NPM 原有工作流特性的基础上，使之变得更快、更安全、更可靠。
        
        1）yarn 安装当前项目的所有包            
         、、、
         yarn install         
         、、、     
        
        或者：     
        、、、
        yarn        
        、、、
        
        当执行 yarn install 命令时，Yarn 会先判断当前文件夹中是否存在 yarn.lock 文件，存在的话会按照文件中特定的包版本进行安装，
        否则读取  package.json 文件中的内容并发送到服务器上解析，解析成功后把结果写入 yarn.lock 文件中，最后安装扩展包。 Laravel
        自带 yarn.lock 文件，此文件的作用与 composer.lock 一致，是为了保证项目依赖代码版本号绝对一致而存在的  
    
        2)用yarn 安装指定的包          
        、、、
        yarn add [package]        
        、、、
    
    3. Laravel Mix#        
        Laravel Mix 一款前端任务自动化管理工具，使用了工作流的模式对制定好的任务依次执行。Mix 提供了简洁流畅的 API，让你能够为你的 Laravel
         应用定义 Webpack 编译任务。Mix 支持许多常见的 CSS 与 JavaScript 预处理器，通过简单的调用，你可以轻松地管理前端资源。我们可以在 webpack.mix.js
         文件中制定一些如资源文件的编译、压缩等任务。Laravel 已默认为我们生成了 webpack.mix.js 文件，并集成了 laravel-mix 模块。
    
        1)webpack.mix.js 内容：
        、、、
        const mix = require('laravel-mix');

        mix.js('resources/js/app.js', 'public/js')
           .sass('resources/sass/app.scss', 'public/css');
        、、、    
        
        2)webpack.js    代码分解    
        、、、
        const mix = require('laravel-mix');        
        、、、
        webpack.mix.js 的解析引擎是 Node.js ，在 Node.js 中 require 关键词是对模块进行引用。        
        Mix 提供了一些函数来帮助你使用 JavaScript 文件，像是编译 ECMAScript 2015、模块编译、压缩、
        及简单的合并纯 JavaScript 文件。更棒的是，这些都不需要自定义的配置。

        、、、
        mix.js('resources/js/app.js', 'public/js')         
        、、、

        以上这一行简单的代码，支持：

        ECMAScript 2015 语法；
        Modules；
        编译 .vue 文件；
        针对生产环境压缩代码。    
        js 方法的第二个参数可以用来自定义生成的 JS 文件的输出目录。   
    
    
        、、、
        mix.sass('resources/sass/app.scss', 'public/css');             
        、、、
        sass 方法可以让你将 Sass 文件编译为 CSS，你可以使用第二个参数来自定义生成的 CSS 的输出目录。    

    4.开始使用 Mix#            
        1)安装Mix npm 依赖
        、、、
        yarn install        
        、、、    
    
        2)Mix 任务管理    
        、、、
        npm run watch-poll        
        、、、 

        watch-poll 会在你的终端里持续运行，监控 resources 文件夹下的资源文件是否有发生改变。在 
        watch-poll 命令运行的情况下，一旦资源文件发生变化，Webpack 会自动重新编译。
        
        在后面的课程中，我们需要保证 npm run watch-poll 一直处在执行状态中。

####    Saas浏览器缓存处理
    Laravel Mix 给出的方案是为每一次的文件修改做哈希处理。
    1)webpack.mix.js 稍作修改 增加了 version() 函数的调用
    、、、
    const mix = require('laravel-mix');

    mix.js('resources/js/app.js', 'public/js')
       .sass('resources/sass/app.scss', 'public/css').version();
    、、、
    
    2)修改 resources/views/layouts/default.blade.php
    、、、
        <!DOCTYPE html>
        <html>
          <head>
            <title>@yield('title', 'Weibo App') - Laravel 入门教程</title>
            <link rel="stylesheet" href="{{ mix('css/app.css') }}">
          </head>
          <body>
        
            <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
              <div class="container">
                <a class="navbar-brand" href="/">Weibo App</a>
                <ul class="navbar-nav justify-content-end">
                  <li class="nav-item"><a class="nav-link" href="/help">帮助</a></li>
                  <li class="nav-item" ><a class="nav-link" href="#">登录</a></li>
                </ul>
              </div>
            </nav>
        
            <div class="container">
              @yield('content')
            </div>
          </body>
        </html>
    、、、
    
    

    以上代码只是做了这一行的修改
    、、、
    <link rel="stylesheet" href="{{ mix('css/app.css') }}">
    、、、

    //mix() 方法与 webpack.mix.js 文件里的逻辑遥相呼应。
    注意：webpack.mix.js 文件只在 npm run watch-poll 指令执行时引入，
    之后指令后台运行不再重新引入。如果你后台运行 watch-poll 命令的话，
    需关闭 watch-poll 服务（Ctrl + C），再次启动（ npm run watch-poll ）即可生效。

####    Git 代码版本控制#
    、、、
    git add -A
    git commit -m "静态文件浏览器缓存问题"
    、、、

####    局部视图
    头部和底部视图#
    1)新建一个头部视图文件 resources/views/layouts/_header.blade.php
    、、、
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container ">
        <a class="navbar-brand" href="/">Weibo App</a>
        <ul class="navbar-nav justify-content-end">
          <li class="nav-item"><a class="nav-link" href="/help">帮助</a></li>
          <li class="nav-item" ><a class="nav-link" href="#">登录</a></li>
        </ul>
      </div>
    </nav>
    、、、
    
    文件名前面加了下划线 _，这样做是为了指定该视图文件为局部视图


    2)创建一个底部视图，用于置放网站的一些基础信息。
    resources/views/layouts/_footer.blade.php
    、、、
    <footer class="footer">
      <img class="brand-icon" src="https://cdn.learnku.com/uploads/sites/KDiyAbV0hj1ytHpRTOlVpucbLebonxeX.png">
      <a href="https://learnku.com/laravel/courses" target=_blank>
        刻意练习，每日精进
      </a>
    
      <div class="float-right">
        <a href="/about" >关于</a>
      </div>
    </footer>
    、、、
    
    
    3）样式优化#
    针对底部视图进行样式优化 resources/sass/app.scss
    、、、
    /* footer */
    
    footer {
      margin-top: 45px;
      padding-top: 5px;
      border-top: 1px solid #eaeaea;
      color: #777;
      font-size: 13px;
      font-weight: bold;
    
      a {
        color: #555;
      }
    
      a:hover {
        color: #222;
      }
    
      img.brand-icon {
        width: 17px;
        height: 17px;
      }
    }

   、、、
    
    4)引入局部视图#
    在完成头部视图和底部视图的定义后，接下来便可以在 default 视图中引用这两个视图。
    resources/views/layouts/default.blade.php
    、、、
    <!DOCTYPE html>
    <html>
      <head>
        <title>@yield('title', 'Weibo App') - Laravel 入门教程</title>
        <link rel="stylesheet" href="{{ mix('css/app.css') }}">
      </head>
    
      <body>
        @include('layouts._header')
    
        <div class="container">
          <div class="offset-md-1 col-md-10">
            @yield('content')
            @include('layouts._footer')
          </div>
        </div>
      </body>
    </html>
    、、、
    
    @include 是 Blade 提供的视图引用方法，可通过传参一个具体的文件路径名称来引用视图。

####    Git 代码版本控制#
    接着让我们将本次更改纳入版本控制中：
    、、、
    git add -A
    git commit -m "切割头部和尾部子视图"
    、、、


####    布局中的链接






























































