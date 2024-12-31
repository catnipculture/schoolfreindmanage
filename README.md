> #### 作者主页：[舒克日记](https://blog.csdn.net/cativen)
>
>  简介：Java领域优质创作者、Java项目、学习资料、技术互助
>
> <b><font color=red>文中获取源码</font></b>

# 校友管理系统项目说明

​

本系统是一个学校与毕业生的交流平台。方便校友们了解母校的最新动态，同学的情况；同时学校也可以通过平台了解毕业生的就业状况等等。根据具体的需求。

本系统包括了校友管理、新闻、行业联谊、捐赠这四大功能模块。

## 校友管理系统部署说明

> 线上访问地址（后台）：localhost:9200
> 
> 线上访问地址（前台）：localhost:9100/index



# 运行指导

idea导入源码空间站顶目教程说明(Vindows版)-ssm篇：

http://mtw.so/5MHvZq 

源码地址：[http://www.codegym.top](http://www.codegym.top/)

## 技术栈

SpringBoot、MybatisPlus、Thymeleaf、MySQL、阿里云OSS、[光年后台管理模板](https://gitee.com/yinqi/Light-Year-Admin-Template)



## 本地部署

1.在mysql中新建数据库xiaoyou，将xiaoyou.sql导入该数据库。

2.打开IDEA，导入此项目， 打开xiaoyou3\xiaoyou_manage\src\main\resources\application.yml 和xiaoyou3\xiaoyou_index\src\main\resources\application.yml的配置文件， 修改数据库用户名和密码为自己本地数据库的用户名和密码，修改数据库地址为本机的对应数据库地址如下：

spring:  
datasource:  
#数据库地址  
url: jdbc:mysql://localhost:3306/xiaoyou?serverTimezone=GMT%2B8  
type: com.alibaba.druid.pool.DruidDataSource  
#mysql的账号  
username: root  
#mysql的密码  
password: root  
driver-class-name: com.mysql.jdbc.Driver

3.配置阿里云OSS图片服务（可选操作）：

在xiaoyou3\xiaoyou_tools\src\main\java\com\lgy\tools\common\utils下配置阿里云OSS服务（建议使用自己的，个人的流量耗不起哈哈哈哈，也不知道什么时候到期了就挂了），参考教程：[阿里云OSS图片服务配置](https://juejin.cn/post/6844904158626070542)

4.邮件服务配置（可选操作）：

在xiaoyou3\xiaoyou_tools\src\main\java\com\lgy\tools\common\utils下的MailUtils类中配置如下：

附：主要是更改邮箱服务器和你的邮箱账号和密码（当然你也可以不改，我的邮箱用多了可能就被视为垃圾邮箱账号了）

package com.lgy.tools.common.utils;

import javax.mail.*;  
import javax.mail.internet.AddressException;  
import javax.mail.internet.InternetAddress;  
import javax.mail.internet.MimeMessage;  
import java.util.Properties;

public class MailUtils {

//邮件发送协议  
private final static String PROTOCOL = "smtp";  
//SMTP邮件服务器（这里使用的是QQ邮箱也可以使用其他的）  
private final static String HOST = "smtp.qq.com";  
//是否要求身份验证  
private final static String IS_AUTH = "true";  
// 是否启用调试模式（启用调试模式可打印客户 端与服务器交互过程时一问一答的响应消息）  
private final static String IS_ENABLED_DEBUG_MOD = "true";  
/**

- @param mailAddress 收件人地址
- @param mailMsg     邮件正文
- @throws MessagingException
- @throws AddressException  
  */  
  public static void sendMail(String mailAddress, String mailMsg,String mailContent) throws MessagingException {  
  // -- 1.创建一个Properties对象.里面 封装基本协议和数据  
  Properties props = new Properties();  
  // -- 设置邮件的发送协议  
  props.setProperty("mail.transport.protocol", PROTOCOL);  
  // -- 设置发送邮件的服务器地址  
  props.setProperty("mail.smtp.host", HOST);  
  // -- 设置发送邮件需要验证  
  props.setProperty("mail.smtp.auth", IS_AUTH);  
  props.setProperty("mail.debug", IS_ENABLED_DEBUG_MOD);  
  //-- 提供验证器  
  Authenticator auth = new Authenticator() {  
  @Override  
  protected PasswordAuthentication getPasswordAuthentication() {  
  // TODO Auto-generated method stub  
  //更改成自己的账号和密码(不是QQ密码)  
  return new PasswordAuthentication("921650190@qq.com", "qreuugzpvxkebefd");  
  }  
  };  
  //-- 开启和服务器的会话  
  Session session = Session.getDefaultInstance(props, auth);  
  //-- 创建消息对象.一个Message对象就 是一封邮件的内容  
  Message msg = new MimeMessage(session);  
  //-- 设置邮件的发送者（自己的邮箱）  
  msg.setFrom(new InternetAddress("921650190@qq.com"));  
  //-- 设置邮件的发送方式和接受者  
  msg.setRecipient(Message.RecipientType.TO, new InternetAddress(mailAddress));  
  //设置邮件的主题  
  msg.setSubject(mailMsg);  
  //设置邮件的正文  
  String url = "http://localhost:9200/index";  
  String content = mailContent+"请去官网查看更多[" + url + "](https://codegym.top/admin/%22%20+%20url%20+%20%22)";  
  msg.setContent(content, "text/html;charset=utf-8");  
  //-- 创建Transport用于发送邮件  
  Transport.send(msg);  
  }

}

5.运行xiaoyou3\xiaoyou_index\src\main\java\com\lgy\xiaoyou_index\下的XiaoyouIndexApplication.java类，启动前台。

6.运行xiaoyou3\xiaoyou_manage\src\main\java\com\lgy\xiaoyou_manage\下的XiaoyouManageApplication.java类，启动后台。

7.打开浏览器，输入 localhost:9200 进入后台登录界面；输入localhost:9100/index进入前台首页。

8.输入用户名和密码访问系统。

## 运行说明

### 1.运行环境：

JDK1.8；Tomcat9.0；MySQL5.5

### 2.账号密码：

管理员账号： 111

管理员密码： 123

普通用户账号：2020

普通用户密码：2020

### 3.访问：

在启动之后访问localhost:9200进入后台登录界面，输入管理员账户名密码进行登录，登录成功便可使用后台系统；访问localhost:9100/index进入前台首页，点击右上角登录按钮，输入普通用户账户名密码进行登录，成功即可使用前台。

## 系统展示

###

### 1.前台部分界面

![前台界面](https://img-blog.csdnimg.cn/img_convert/a034c6274dd3165adb60dffdecb99e62.png)

###

### 2.后台部分界面

![后台](https://img-blog.csdnimg.cn/img_convert/80eae60c96d17b78292f1beed5064810.png)

![部分系统截图1](https://img-blog.csdnimg.cn/img_convert/6593dabdddeae2a117a1dcd8504f0e6a.png)
