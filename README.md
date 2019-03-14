> 前几天搞了一个文件管理系统，因为几乎做每一个项目都涉及到上传文件这一步骤，不可能每一个项目都做一个模块处理文件，所以我最近整了一个小文件系统来用，这样子别的项目上传文件的话，直接可以上传到该项目即可。。。

整体效果，如下：
#### 项目结构
<a href="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313233907508.jpg" target="_blank">
<img src="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313233907508.jpg" alt="查看大图" />
</a>

#### 首页效果

<a href="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313222119329.png" target="_blank">
<img src="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313222119329.png" alt="查看大图" />
</a>

#### 日志查看

<a href="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313222544156.jpg" target="_blank">
<img src="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313222544156.jpg" alt="查看大图" />
</a>

#### (1)解决了什么问题？

 - 简化其他项目的文件处理（上传 | 下载）问题，统一处理
 - 个人的小云盘，并且可以提供外链访问下载等

> 这个文件系统主要功能其中包括`上传文件`、`下载文件`、`在线观看`、`删除文件`、`文件检索`、`访问监控`、`防盗链`等
> 其中文件是存储在七牛云服务器上的，简要介绍一下，七牛云有10G的对象存储空间可以使用,永久的,支持http,不提供https流量,所以这也是我撘文件系统的原因之一，就是为了小程序的https....否则小程序无法访问图片

#### 防盗链效果

<a href="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313225348446.png" target="_blank">
<img src="https://shaines.cn/comments/view?filename=https://img-blog.csdnimg.cn/20190313225348446.png" alt="查看大图" />
</a>
but 对于爬虫来说无任何阻碍【捂脸】

#### (2)用到的技术栈
 - ##### 前端
   - freemarker
   - bootstrap
   - bootstrap-table
   - jquery
 - ##### 后台
   - springboot 2.1.3.RELEASE
   - spring-data-jpa 2.1.3.RELEASE
   - mysql 5.7

 - ##### 搭建
    - tomcat 9.0.1 (or 7.0)
    - maven 3.5.4

 - ##### 其他依赖
    - qiniu[7.2.0, 7.2.99]
    - fastjson 1.2.54


#### (3)未来的期望
暂时的话不想继续完善了，先实习然后学习一段时间先，基本功能差不多，继续添加的功能的话，就是为了用技术而作了，等有时间了会考虑继续迭代吧

- 多用户(用户管理)
- 文件管理(文件签名)
- 权限控制（spring security）
- 分布式文件存储（hadoop HDFS）：正在学习中...

#### (4)哪里下载

* [github](https://github.com/HouYuSource/filesystem.git)

导入注意事项:

 1. sql文件

    修改 application.properties
    ```properties
    spring.jpa.hibernate.ddl-auto=create-drop # 自动创建表
    ```
	
 2. 修改数据库
	```properties
    spring.datasource.url=jdbc:mysql://localhost/{database}?characterEncoding=utf-8&useSSL=false&serverTimezone=UTC
    ```
 3. 七牛云配置

    前往[七牛云官网](https://portal.qiniu.com)注册账号,并且获取绑定好域名,如果不绑定,七牛云提供一个月的免费域名,一个月后失效,建议绑定自己的,前往[对象存储](https://portal.qiniu.com/bucket)创建`Bucket`,并且获取`accessKey` `secretKey` `domainOfBucket`在util.QiniuUtil.java文件中修改对应的配置即可。
    ```java
	private static final String accessKey = "your accessKey";
    private static final String secretKey = "your secretKey";
    private static final String bucket = "your bucket";
    private static final Configuration cfg = new Configuration(Zone.zone0());
    private static final String domainOfBucket = "your domainOfBucket";
    ```

##### 交流
博客同步到[SHY BLOG](https://www.shaines.cn)
mail ：for.houyu@qq.com
