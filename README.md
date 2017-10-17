# crackGFW
In this tutorial, I will introduce the procedures to set up shadowsocks tp jump the Great Fire Wall in China.
Apart from the shadowsocks, we also need to have a VPS as the server, and we use Digital Ocean in this article.


## Set up Digital Ocean
* Students can get $50 credits from [education pack](https://education.github.com/pack) (if you do not have github account, please register with your university email), then you can get the promo code from the https://education.github.com/pack/offers#digitalocean like
* ![alt tag](/images/50credit.png)
* Then go to the [Digital Ocean](https://www.digitalocean.com/) to register an account. 
Note that you may need to bind your credit card or use Paypel to pay $5 to finish the registration.
* After that, create a droplet by selecting CentOS, $5/Month size (it is enough for this work), New York (or other places by testing speed in http://speedtest-nyc3.digitalocean.com/).
* ![alt tag](/images/centos.png)
![alt tag](/images/size.png)
![alt tag](/images/dataCenter.png)
* Finally, you should get the IP address of the server as:
*![alt tag](/images/droplet.png)
* You can ping the IP address by the cmd in windows to check if you can access to the server.
If so, you can get results like 
![alt tag](/images/ping.png)
* You will also get the password from the email sent to you.

## Set up Shadowsocks server
* Download [Putty](http://www.putty.org/) and then open the software and type "root@yourIP" in the new session.
And then type the password, and then create new password for your server.
* ![alt tag](/images/putty.png)
* Install all dependencies:
```bash
yum install python-setuptools && easy_install pip
pip install shadowsocks
```
* Then set up the shadowsocks by creating a configuration file:
```bash
vi /etc/ssconfig.json
```
Press 'i' for the insert mode and copy the following content:
```
{
    "server": "yourServerIP", 
    "server_port": 8388,
    "local_port": 1080, 
    "password": "yourPassword", 
    "timeout": 600,
    "method": "aes-256-cfb",
    "fast_open": false
}
```
After that, click "ESC" button, and type ":wq" to save and quit.
Finally, we launch the server in the background by typing 
```bash
ssserver -c /etc/ssconfig.json -d start
```
You can check whether your server successfully runs by typing 
```bash
netstat -antlp | grep 8388
```
and the results should be like
* ![alt tag](/images/listen.png)


## Set up the shadowsocks client
* Download the client from https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.0.6/Shadowsocks-4.0.6.zip 
* Install and fill in the content by 
* ![alt tag](/images/clientConfig.jpg)
* Then set the client as global proxy i.e.,
* ![alt tag](/images/globalProxy.jpg)
* Now you can try to access to Google, Twitter, Youtube ... in your browser in the windows. 
You can also download the client for different platforms (Already successfully tested):
  * [Mac new](https://github.com/shadowsocks/ShadowsocksX-NG/releases)
  * [Mac old](https://github.com/shadowsocks/shadowsocks-iOS/releases/)
  * [Android](https://github.com/shadowsocks/shadowsocks-android/releases)

## PAC file
PAC (Proxy auto-config) is used to show that what websites that we need to use shadowsocks.
Because it will be faster to directly visit Chinese websites without Shadowsocks.
So, you can add all websites that you cannot access directly or slowly into the pac.txt.
The rules are explained in detail in http://www.cnblogs.com/edward2013/p/5560836.html .


## TODOS:
* Intelligent PAC tool like MEOW https://www.loyalsoldier.me/an-easy-guideline-to-fuck-the-gfw/
* Speed up the server such as
  * http://yooooh.net/2015/10/10/ipv6-shadowsocks/
  * http://www.liwenqiao.com/p/shadowsocks-digitalocean-build/
  * https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks

## Other tutorials
* https://www.loyalsoldier.me/fuck-the-gfw-with-my-own-shadowsocks-server/
* https://www.iwwenbo.com/digitalocean-shadowsocks/

	
