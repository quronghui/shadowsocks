# By github student pack build VPN
+ [总过程](http://tzaiyang.me/Free-Unlimited-Internet-Access-For-CERNET-Users/)
## 1、注册github学生账号
+ [注册学生账号，领取学生包](https://www.jianshu.com/p/56323405509c)
+ [学生包](https://education.github.com/pack)
## 2、注册注册PayPal账号
+ [paypal官网](https://www.paypal.com/c2/webapps/mpp/home?locale.x=zh_c2)
+ 注册个购买账户，需要用到身份证等信息，绑定一张能开网银的银行卡
## 3、注册DigitalOcean账号
+ [注册账号](https://www.digitalocean.com/github-students/?utm_medium=partnerships&utm_source=github&utm_campaign=studentdevpack)
+ Need 邮箱和密码，验证邮箱
+ 193@qq.com --quronghui5
## 4、领取优惠券并且购买
+ [登录github student pack](https://www.jianshu.com/p/56323405509c)
+ 购买、配置VPS --选择CentOS
- 记住用户名和密码
+ Droplet Name: ubuntu-s-1vcpu-1gb-sfo2-01
+ IP Address: 165.227.50.173
+ Username: root
+ Password: quronghui5
+ 
+    "server":"165.227.50.173",  
+    "local_address":"127.0.0.1",  
    "local_port":1080,  
    "port_password":{  
         "8096":"quronghui5",  
         "8097":"quronghui5",  
         "8098":"quronghui5",  
         "8099":"quronghui5",  
         "8100":"quronghui5",  
    },  
    "timeout":300,  
    "method":"aes-256-gcm",  
    "fast_open":false  
}  
## 多用户搭建不成功
+ 只能用第一个客户端    
+ 多台电脑的配置，我采用的是将配置文件复制过去  
+ 实现连接  
## 5、VPN搭建SS
+ ssh root@IP Address: (165.227.50.173)-password:quronghui5
+ [一键搭建](https://teddysun.com/342.html)
+ [linux下的优化](https://www.polarxiong.com/archives/Ubuntu-16-04%E4%B8%8BShadowsocks%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E5%AE%89%E8%A3%85%E5%8F%8A%E4%BC%98%E5%8C%96.html)
+ 选其一
+ 选用的是[一键搭建]，ubuntu上搭建远程服务器，本地电脑通过shadowsocks进行联网
## 6、本地shadowsocks测试
+ [本地测试](https://www.jianshu.com/p/509c696ee838)
+ Enjoy!

## 免费的git vpn

1. 当我自己的vpn到期后；
2. 将原来的gui-config.json文件，用free-gui-config.json替换就行。