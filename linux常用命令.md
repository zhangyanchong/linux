	1.  linux 处理文件的速度刚刚的 
	cat  UserDataAll_*_log_20160306.log UserDataAll_*_log_20160307.log UserDataAll_*_log_20160308.log  | grep '4.5.021' | grep '"event_id":20000,"event_type":2,' | grep '"user_id":0' |  awk -F '"device_id":"' '{print $2}' | awk -F '","' '{print $1 ,$17}' |  awk -F 'time":"' '{print $1 ,strftime("%Y-%m-%d",$2)}'  | grep -i "[a-zA-Z0-9]\{1,40\}.*2016-03-07" | sort -u | grep . -c
	
	解释
	  cat      将 文件输出到屏幕中  （匹配很多日志）
	            将UserDataAll_*_log_20160306.log   *匹配任意字符  将2016 3月6日的 所有的 UserDataAll 这样的日志
	            将UserDataAll_*_log_20160307.log   *匹配任意字符  将2016 3月7日的 所有的 UserDataAll 这样的日志
	  grep   管道过滤  一行一行过滤
	  awk    很强大 （可以抽空看看）      
	           awk - F  '"device_id"'  是以 "device_id"  分割   行的字符串 
	           '{print $2}'  打印 出匹配到的第二个  
	           strftime  将时间戳转化成字符串
	  grep -i  不区分大小写
	         "[a-zA-Z0-9]\{1,40\}.*2016-03-07"  正则匹配 注意斜杠
	  sort -u  去重复的
	  grep .  -c  匹配字符  统计次数
	
	
	
	
	
	//牛逼命令
	grep -rl "10.10.10.134" *   查找当前文件中 含有‘10.10.10.134’  的文件列表
	
	
	
	netstat -anp | grep 端口号    查看端口占用效果

    top -p   进程id  当前进程占用内存 和cpu 情况