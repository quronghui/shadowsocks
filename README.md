# Shadowsocks

+ 自己搭建的服务器容易被封了;
+ 可以使用 hostwinds 或者 淘宝上购买账户;

## [vultr 服务器的购买](https://github.com/wistbean/vpn)

1. 购买服务器:获取服务器的ip和密码

## 服务器端配置

+ 登录我们申请成功的IP

  ```
  $ ssh root@IP Address: (104.238.160.173)	
  $ sudo passwd		// 修改密码
  ```
  
+ 搭建shadowsocks服务器

  ```
  $ wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
  $ chmod +x shadowsocks.sh	// 给权限
  $ ./shadowsocks.sh 2>&1 | tee shadowsocks.log	// 选择配置
  ```

+ 搭建成功的提示  

  ```
  Welcome to visit:https://teddysun.com/342.html
    Enjoy it!
  ```

+  基本的修改命令
  ```
  启动：/etc/init.d/shadowsocks start
  停止：/etc/init.d/shadowsocks stop
  重启：/etc/init.d/shadowsocks restart
  状态：/etc/init.d/shadowsocks status
  ```
## 客户端配置

### windows 

+ 下载后，打开ss客户端，按服务器端信息进行配置，配置完成后。
+ 在通知栏（一般默认隐藏到通知栏运行）找到对应的图标，右击使能代理，到此大功告成，测试google应该能正常访问了。

### [ubuntu配置 shadowsocks](http://tanqingbo.com/2017/07/19/Ubuntu使用shadowsocks翻墙/)

+ 加入server服务器内容

  ```
    {
        "server":"104.238.160.173",
        "server_port":9966,
        "local_address": "127.0.0.1",
        "local_port":1080,
        "password":"quronghui",
        "timeout":300,
        "method":"aes-256-gcm",
        "fast_open": false  
    }
    //server 你服务端的IP
    servier_port 你服务端的端口
    local_port 本地端口，一般默认1080
    passwd ss服务端设置的密码
    timeout 超时设置 和服务端一样
    method 加密方法 和服务端一样
  ```

+  简单链接和测试

  ```
$ sudo sslocal -c /shadowsocks/shadowsocks.conf -d start  // stop 是停止的命令
  ```

   + 报错1：ERROR method aes-256-gcm not supported

     + pypi 的 2.8.2 不支持

     ```
     pip install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U
     ```

   + 报错2 

     ```
     2015-02-16 23:59:07 INFO starting local at 127.0.0.1:1080  
     ERROR [Errno 98] Address already in use
     ```

     + 这个只是1080端口号被使用了，重新分配一个就行了，改成1082都行
     + 当时配置的时候一直再找错误，不知道怎么回事

   + 报错3 

     ```
     服务器的开启
     	ssserver -c /etc/shadowsocks/config.json -d start
     本地客户端的链接
     	sslocal -c /etc/shadowsocks/config.json -d start
     	在本地客户端这里要用sslocal
     ```

4. 设置开机自启动ss客户端，连接服务器

   + apt-get supervisor
   + 在客户端下的登录是sslocal

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

5. **如何查看是否连接成功**

   ```
   查看日志:我们在下面的配置哪里，建立了shadowsockets.log
   	vi /var/log/shadowsockets.log
   ```

   

## 配置chrome浏览器

1. 如果在chrome的扩展中添加不了Proxy SwitchyOmega?

   + 先设置成全局代理; 然后在在chrome扩展中搜索安装;

   ![全局代理设置](https://github.com/quronghui/shadowsocks/blob/master/proxy全局代理.png)

   + [或者在github上下载](https://github.com/XX-net/XX-Net/tree/master/SwitchyOmega)

2. 配置SwitchyOmega 中的proxy: 实现PAC代理

   ![配置proxy](https://github.com/quronghui/shadowsocks/blob/master/proxy_PAC代理.png)

