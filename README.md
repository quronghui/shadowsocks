# By github student pack build VPN
+ [总过程](http://tzaiyang.me/Free-Unlimited-Internet-Access-For-CERNET-Users/)

## VPN账号的申请

1. 注册github学生账号
   + 注册github学生包账号，可以领取一年左右的权限，免费使用shadowsocks
   + [学生包](https://education.github.com/pack)

2. 注册注册PayPal账号

   + 注册个购买账户，需要用到身份证等信息，绑定一张能开网银的银行卡
   + 用于给服务器VPN缴费

   + [paypal官网](https://www.paypal.com/c2/webapps/mpp/home?locale.x=zh_c2)

3. 注册DigitalOcean账号
   + 用于管理VPN账号的
   + [注册账号](https://www.digitalocean.com/github-students/?utm_medium=partnerships&utm_source=github&utm_campaign=studentdevpack)
   + 193@qq.com 

4. 领取优惠券并且购买

   + 登录github student pack

   + 选择Digital Ocean,领取50m美元

   + 购买、配置VPS --选择CentOS

   + 记住用户名和密码

     ```
     - Droplet Name: ubuntu-s-1vcpu-1gb-sfo2-01
     - IP Address: 165.227.50.173
     - Username: root
     - Password: quronghui5
     - "server":"165.227.50.173",  
     - "local_address":"127.0.0.1",  
           "local_port":1080,  
       "port_password":{  
            "8096":"quronghui5",  
       },  
       "timeout":300,  
       "method":"aes-256-gcm",  
       "fast_open":false  
       }  
     ```

## VPN账号搭建Shadowsocks 代理

+ 登录我们申请成功的IP

  ```
  ssh root@IP Address: (165.227.50.173)
  	password:quronghui5	
  ```

  + 登陆成功后的操作界面是不同

  + 操作的用户名是Digital Ocean申请的用户名

    {% asset_img sshlogin.png %}

+ 选其一搭建服务器

  + [一键搭建](https://teddysun.com/342.html)

    ```
    wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
    chmod +x shadowsocks.sh
    ./shadowsocks.sh 2>&1 | tee shadowsocks.log
    ```

  + [linux下的优化](https://www.polarxiong.com/archives/Ubuntu-16-04%E4%B8%8BShadowsocks%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E5%AE%89%E8%A3%85%E5%8F%8A%E4%BC%98%E5%8C%96.html)

  + 选用的是 **一键搭建**，ubuntu上搭建远程服务器，本地电脑通过shadowsocks进行联网

+ 搭建成功后

  ```
  Welcome to visit:https://teddysun.com/342.html
  Enjoy it!
  ```

+ 基本的修改命令

  ```
  启动：/etc/init.d/shadowsocks start
  停止：/etc/init.d/shadowsocks stop
  重启：/etc/init.d/shadowsocks restart
  状态：/etc/init.d/shadowsocks status
  ```

+ 开机自启动的设置

  ```
  sudo vim /etc/init.d/rc.local	//这个文件自己创建的
  add : /etc/init.d/shadowsocks start
  ```

+ reboot 测试

  ```
  状态：/etc/init.d/shadowsocks status
  ```

## 本地搭建shadowsock 客户端

### windows 

+ 下载后，打开ss客户端，按服务器端信息进行配置，配置完成后。
+ 在通知栏（一般默认隐藏到通知栏运行）找到对应的图标，右击使能代理，到此大功告成，测试google应该能正常访问了。

### Linux 

1. 安装shadowsocks客户端:

   ```
   sudo apt install shadowsocks
   sslocal 		//查看是否安装成功
   ```

2. 配置连接

   + 建立一个shadowsocksjson文件

     ```
     vim /home/quronghui/shadowsocks/shadowsocks.json	//路径任选
     ```

   + 加入server服务器内容

     ```
     {
         "server":"165.227.50.173",
         "server_port":8080,
         "local_port":1080,
         "password":"quronghui",
         "timeout":300,
         "method":"aes-256-gcm",
     }
     // 和shadowsocks的.json文件一样
     ```

3. 设置开机自启动ss客户端，连接服务器

   + apt-get supervisor

   ```
   sudo apt-get install supervisor
   sudo vim /etc/supervisor/supervisord.conf、
   add:
       [program:shadowsocks]
       command=sslocal -c /home/quronghui/shadowsocks/shadowsocks.json
       autostart=true
       autorestart=true
       user=root
       log_stderr=true
       logfile=/var/log/shadowsocks.log
   ```

   + restart

     ```
     sudo service supervisor restart
     ps -ef|grep sslocal
     ```

   + 设置开机自启动

     ```
     sudo vim /etc/rc.local		//我这个文件是自己建立的
     add:	
     	service supervisor start 
     ```

   + reboot 测试是否成功

     + ping 服务器的ip地址

     {% asset_img pingshadowsocks.png %}

## 免费的gui-config.json

1. windows下我是可以找到配置文件
   + 将原来的gui-config.json文件，用free-gui-config.json替换就行。
2. ubuntu下的配置文件我没有找到confi