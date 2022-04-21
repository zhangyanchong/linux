linux  开机启动

编写此文件:/etc/rc.d/rc.local

   /usr/bin/php-fpm &   
   sync --daemon  



最后给个执行权限
  chmod +x /etc/rc.d/rc.local