---
lyout: post
title: webservice测试
categories: 自动化测试
description: 
keyword: 接口测试
---

## 写在前面

世间万物么有完美的，同样在工作中也是一样，没有完美的工具，如果我们总是依据工具做事，有时候很便捷，但有时候也往往会让我们的工作变的困难。甚至有时候还会阻碍我们前进，当然有时候我们需要沉淀，当我们的东西多了我们才能沉淀出更好的东西，更符合我们的工具。

## websevice的测试

  工具有很多，jmeter，soapUI等等。。。但webservice的接口还是贼麻烦的，所以测试起来倍感麻烦。如果在过程发现很多东西不好弄的话，建议手敲代码搞定(今天多敲一点，敲的多了就有可能沉淀出来一款工具了)

## 具体步骤
1.  访问接口地址如:http://ip:port/xxx/xxx/xxx?wsdl
2.  会出现一个类似于xml的网页
3.  另存为xml
4.  通过使用命令:wsimport -keep [xmlpath]/[xmlfile]
5. 导包
6. 写webservie client
```
	JaxWsProxyFactoryBean bean = new JaxWsProxyFactoryBean();
	
	bean.setAddress("[]?wsdl");
	bean.setAddress("[接口地址]?wsdl");
	    //
	    bean.setServiceClass(IJsfsWebService.class);
	    //
	    IJsfsWebService service = (IJsfsWebService)bean.create();

	    String sfxx = "";
	    String ywdm = "";
	    String data = "";
	    String s = service.ywxtPush(sfxx,ywdm,data,s1Md5);
	    System.out.println(s);
```

这就是简单的实现webservice client的实现代码，这样的话就可以方便的做很多事情，当然如果工具能轻易完成的，我们是不建议写代码，但是工具如果不具备，或者用起来比较勉强，我建议还是动手搞定我们的事情。
