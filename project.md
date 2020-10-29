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


##  页面优化部分

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

