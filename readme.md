<img src="https://avatars.githubusercontent.com/u/56885001?s=200&v=4" alt="logo" width="130" height="130" align="right"/>

[![](https://img.shields.io/badge/TgChat-@UnOfficialV2board讨论-blue.svg)](https://t.me/unofficialV2board)



## 安装Redis、fileinfo#
 - aaPanel 面板 > App Store > 找到PHP 7.4点击Setting > Install extentions > redis,fileinfo 进行安装。

## 解除被禁止的函数#
 - aaPanel 面板 > App Store > 找到PHP 7.4点击Setting > Disabled functions 将 putenv proc_open pcntl_alarm pcntl_signal 从列表中删除。

## 安装V2Board#
 - 通过SSH登录到服务器后访问站点路径如：/www/wwwroot/你的站点域名。

 - 以下命令都需要在站点目录进行执行。

## 删除目录下文件
 - chattr -i .user.ini
 - rm -rf .htaccess 404.html index.html .user.ini
 - 执行命令从 Github 克隆到当前目录。

 - git clone https://github.com/wyx2685/v2board.git ./
## 执行命令安装依赖包以及V2board

 -  sh init.sh
## 根据提示完成安装


## 配置站点目录及伪静态#
添加完成后编辑添加的站点 > Site directory > Running directory 选择 /public 保存。

添加完成后编辑添加的站点 > URL rewrite 填入伪静态信息。


location /downloads {
}

location / {  
    try_files $uri $uri/ /index.php$is_args$query_string;  
}

location ~ .*\.(js|css)?$
{
    expires      1h;
    error_log off;
    access_log /dev/null; 
}


##配置定时任务#
aaPanel 面板 > Cron。

在 Type of Task 选择 Shell Script
在 Name of Task 填写 v2board
在 Period 选择 N Minutes 1 Minute
在 Script content 填写 php /www/wwwroot/路径/artisan schedule:run

根据上述信息添加每1分钟执行一次的定时任务。

##启动队列服务#
V2board的系统强依赖队列服务，正常使用V2Board必须启动队列服务。下面以aaPanel中supervisor服务来守护队列服务作为演示。

aaPanel 面板 > App Store > Tools

找到Supervisor进行安装，安装完成后点击设置 > Add Daemon按照如下填写

在 Name 填写 V2board
在 Run User 选择 www
在 Run Dir 选择 站点目录 在 Start Command 填写 php artisan horizon 在 Processes 填写 1

填写后点击Confirm添加即可运行。
## 本分支支持的后端
 
 - [修改版XrayR](https://github.com/wyx2685/XrayR)
 - [修改版V2bX](https://github.com/wyx2685/V2bX)
 - [V2bX](https://github.com/InazumaV/V2bX)

## 原版迁移步骤

按以下步骤进行面板文件迁移：

    git remote set-url origin https://github.com/wyx2685/v2board  
    git checkout master  
    ./update.sh  


按以下步骤刷新设置缓存，重启队列:

    php artisan config:clear
    php artisan config:cache
    php artisan horizon:terminate

最后进入后台重新保存主题： 主题配置-主题设置-确定

# **V2Board**

- PHP7.3+
- Composer
- MySQL5.5+
- Redis
- Laravel

## Demo
[Demo](https://demo.v2board.com)

## Document
[Click](https://v2board.com)

## Sponsors
Thanks to the open source project license provided by [Jetbrains](https://www.jetbrains.com/)

## Community
🔔Telegram Channel: [@v2board](https://t.me/v2board)  

## How to Feedback
Follow the template in the issue to submit your question correctly, and we will have someone follow up with you.
