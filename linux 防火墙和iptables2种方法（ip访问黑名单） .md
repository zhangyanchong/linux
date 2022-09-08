# linux 防火墙和iptables  2种方法 


    查看状态
    firewall-cmd --state
    
    拒绝访问
    firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="49.232.8.38" port protocol="tcp" port="80" reject"
    
    重新载入一下防火墙设置，使设置生效
    firewall-cmd --reload
    
    查看已设置的规则
    firewall-cmd --zone=public --list-rich-rules
    
    
    删除拒绝访问
    firewall-cmd --permanent --remove-rich-rule="rule family="ipv4" source address="49.232.8.38" port protocol="tcp" port="80" reject"
    
    重新载入一下防火墙设置，使设置生效
    firewall-cmd --reload




—————————————————————————————————————————————————————————————————————




    有这个就可以 iptables
    yum list installed | grep iptables
    
    iptables -L INPUT  命令是否有
    
    拒绝访问
    iptables -I INPUT -s 49.232.8.38 -j DROP   
    
    效果是ping 不通   访问web也访问不了
    
    
    删除拒绝访问
    iptables -D INPUT -s 49.232.8.38 -j DROP
    
    
    查看拒绝访问
    iptables -L INPUT  或者 iptables -L 
    
    
    一键清空所有规则
    iptables -F
