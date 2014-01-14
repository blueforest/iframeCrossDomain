在跨域问题上，域仅仅是通过“URL的首部”来识别而不会去尝试判断相同的ip地址对应着两个域或两个域是否在同一个ip上.
参考：http://developer.51cto.com/art/201102/245701.htm

### 一.用代理页面的方法
主页面 www.a.test，嵌套页面:www.b.test
本地apache配置多域名
 - 1.hosts 绑定 
    127.0.0.1 www.a.test
    127.0.0.1 www.b.test
 - 2.apache配置 httpd-vhosts.conf文件配置


```html
<VirtualHost *:80>
    DocumentRoot "/Applications/XAMPP/xamppfiles/htdocs/iframetest/a"
    ServerName www.a.test
   SetEnv RUNTIME_ENVIROMENT DEV
   <Directory "/Applications/XAMPP/xamppfiles/htdocs/iframetest/a">
      Options Indexes FollowSymLinks
      AllowOverride none
      Order allow,deny
      Allow from all         
      RewriteEngine on
      RewriteBase    /
      RewriteCond %{REQUEST_FILENAME}   !-f
      RewriteRule ^(.*)$ index.html [L]
   </Directory>
</VirtualHost>
```
### 二. 用html5 的postMessage
