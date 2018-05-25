 中文分词
第一步  下载  
   https://pan.baidu.com/s/1smOxPhF   下载 ikanalyzer-solr6.5.zip   解压   
   ik-analyzer-solr5-5.x.jar 只要这个放在  /zyc/program/solr/server/solr-webapp/webapp/WEB-INF/lib
  
  第二步  
  解压的 IKAnalyzer.cfg.xml  ext.dic stopword.dic 放在目录 一个配置文件 一个的停词用的
   /zyc/program/solr/server/solr-webapp/webapp/WEB-INF/classes    下面（如果没有classes 新建一个）

 第三步     
  /zyc/program/solr/server/solr/test/conf/managed-schema   fieldType附近添加 大概536行左右
  
	<!-- 配置中文分词器Ik -->
     <fieldType name="text_ik" stored="true" indexed="true" class="solr.TextField" >
          <analyzer type="index" class="org.wltea.analyzer.lucene.IKAnalyzer"/>
          <analyzer type="query" class="org.wltea.analyzer.lucene.IKAnalyzer"/>
     </fieldType>

 第四步  重启solr 服务  
    /zyc/program/solr/bin/solr restart -force
  
  