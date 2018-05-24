solr  导入数据库数据


1 第一步 导入数据导出的jar包
  cp -rf   /zyc/program/solr/dist/solr-dataimporthandler-7.3.1.jar /zyc/program/solr/server/solr-webapp/webapp/WEB-INF/lib  
  cp -rf   /zyc/program/solr/dist/solr-dataimporthandler-extras-7.3.1.jar /zyc/program/solr/server/solr-webapp/webapp/WEB-INF/lib  
2 第二步  
  在此/zyc/program/solr/server/solr/test/conf/solrconfig.xml  <config\>....中</config\>  添加  

	<requestHandler name="/dataimport" class="solr.DataImportHandler">
	   <lst name="defaults">
	      <str name="config">solr-data-config.xml</str>
	   </lst>
	</requestHandler> 

第三步  
  创建solr-data-config.xml文件  路径为：/zyc/program/solr/server/solr/test/conf 内容为  

	<dataConfig>
	  <dataSource name="db1"   
	   driver="com.mysql.jdbc.Driver"     
	   url="jdbc:mysql://127.0.0.1:3306/nbsay"    
	   user="user"       
	   password="passwd"   
	   />   <!--数据库连接--> <!--用户名--> <!--密码-->
	  <document>
	  <entity dataSource="db1" name="contents"  query="select * from content"   > <!--sql 查询-->
	   <field column="id" name="id"/>             <!--solr要查询的field-->
	   <field column="content" name="content"/>   <!--solr要查询的field-->
	  </entity>
	  </document>
	</dataConfig>

第四步
  下载 mysql 驱动包：绝大部分jar包在maven仓库都能找到，mysql驱动包在maven仓库中的下载链接是：http://central.maven.org/maven2/mysql/mysql-connector-java/   
  下载最新即可  
  放在 /zyc/program/solr/server/solr-webapp/webapp/WEB-INF/lib  下面

第五步  
  在managed-schema文件中添加对应于数据库字段的 solr要查询的field  
  找到类似这一块 添加即可     
 
<field name="content" type="text_general" indexed="true" stored="true" /\>
