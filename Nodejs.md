##  搭建Node.js 开发环境

####    解决GitHub的raw.githubusercontent.com无法连接问题

    1.在https://site.ip138.com/raw.Githubusercontent.com/ 
    2.输入raw.githubusercontent.com，查询IP地址     
    
    3.修改hosts Ubuntu，CentOS及macOS直接在终端输入 
      
    、、、
        sudo vi /etc/hosts    
    、、、
    
    4.添加以下内容保存即可 （IP地址查询后相应修改，可以ping不同IP的延时 选择最佳IP地址）
    
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
####    手动新建.bashrc和.bash_profile文件内容

        vim .bashrc            
    、、、
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
        [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    、、、
    
    
        vim .bash_profile
    、、、
        source  ~/.bashrc    
    、、、


####    安装 nvm
    、、、
        curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
    、、、

#### 测试安装结果
    、、、
    nvm --version  //0.33.8
    、、、

    //查看远程 node 版本
    、、、
    nvm ls-remote 
    
    
     v0.1.14
        v0.1.15
        v0.1.16
        v0.1.17
        v0.1.18
        v0.1.19
        v0.1.20
        v0.1.21
        v0.1.22
        v0.1.23
        v0.1.24
        v0.1.25
    、、、

#### 安装最新稳定版 node，当前是 node v15.0.1 (npm v7.0.3)
    、、、
    nvm install stable
    、、、

####   安装 yarn
    、、、
    npm install -g yarn
    、、、