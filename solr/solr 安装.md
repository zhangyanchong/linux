solr7.3 安装   
1 环境要求 java 1.8或者更高
  yum install java  
2 下载solr 包  
  地址 https://mirrors.tuna.tsinghua.edu.cn/apache/lucene/solr/7.3.1/solr-7.3.1.tgz  
  wget  https://mirrors.tuna.tsinghua.edu.cn/apache/lucene/solr/7.3.1/solr-7.3.1.tgz  
  tar  -zxvf   solr-7.3.1.tgz  
3 启动  
  /zyc/program/solr/bin start  -force    //-force  因为的root  
4 页面访问  
  http://198.*.*.179:8983/solr/#/  
5  创建核心或者集合  
   /zyc/program/solr/bin create -c test  
   生成的文件在/zyc/program/solr/server/solr/test  下面  
6 给sorl web 添加登陆密码  (相关文档https://www.bbsmax.com/A/Gkz12Dj6JR/)  
   第一步新建  
  /zyc/program/solr/server/etc/realm.properties  内容   
  test:123,admin  
   第二步   /zyc/program/solr/server/contexts/solr-jetty-context.xml文件如下,文件中插入安全处理程序设置标签

		<?xml version="1.0"?>
		<!DOCTYPE Configure PUBLIC "-//Jetty//Configure//EN" "http://www.eclipse.org/jetty/configure_9_0.dtd">
		<Configure class="org.eclipse.jetty.webapp.WebAppContext">
			<Set name="contextPath"><Property name="hostContext" default="/solr"/></Set>
			<Set name="war"><Property name="jetty.base"/>/solr-webapp/webapp</Set>
			<Set name="defaultsDescriptor"><Property name="jetty.base"/>/etc/webdefault.xml</Set>
			<Set name="extractWAR">false</Set>
			<!-- 安全处理程序设置 此处是添加的 -->
			<Get name="securityHandler">
				<Set name="loginService">
					<New class="org.eclipse.jetty.security.HashLoginService">
					   <Set name="name">TestRealm</Set>  <!-- 一个名字-->
					   <!-- 引入刚刚新建的文件 -->
					<Set name="config"><SystemProperty name="jetty.home" default="."/>/etc/realm.properties</Set>
					</New>
				</Set>
			  </Get>
		</Configure>
 第三步	 /zyc/program/solr/server/solr-webapp/webapp/WEB-INF/web.xml  ,插入

	<security-constraint>
	　　<web-resource-collection>
	    　　<web-resource-name>Solr</web-resource-name> <!--描述-->
	    　　<url-pattern>/</url-pattern>               <!-- 验证的网页的位置-->
	    </web-resource-collection>
	     <auth-constraint>
	        <role-name>admin</role-name>   <!-- 验证的角色，别写成用户名，如有多个角色可以写多个role-name 标签-->
	    </auth-constraint>
	</security-constraint>
	<login-config>
	    <auth-method>BASIC</auth-method><!-- 关键-->
	    <realm-name>TestRealm</realm-name>
	</login-config>  

第四步
  配置完成后,重启solr服务器,重新访问solr就需要用户名和密码了
  
   
