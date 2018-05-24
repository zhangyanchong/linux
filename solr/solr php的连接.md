1 此处直接写的是简单的连接  
  不涉及登陆和密码的

		$rs=file_get_contents("http://123.57.255.131:8984/solr/testsolr/select?hl.fl=content&hl.simple.post=&wt=php");
		echo  "<pre>";print_r($rs);exit;

  涉及登陆和密码的

	$rs=file_get_contents("http://user:passwd@198.13.38.179:8983/solr/test/select?q=*:*");
	echo  "<pre>";print_r($rs);exit;

其中user 为用户名 passw的为密码