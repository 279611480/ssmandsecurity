# ssmandsecurity
SpringBoot整合SSM(全注解   HTML   不使用.xml)  +@Slf4j +SpringSecurity与数据打交道

将自己分支上的（https://github.com/279611480/mySsm）  第二个整合了Log的代码拉下来【这次打算与数据库打交道实现权限控制】，  也可以继续自己的ssm项目创建新的分支，只是之前的项目是 并未与数据库打交道实现用户登录权限  判断 功能，如果在那边新创建分支，但是需要删除一些东西（所以懒得去动，而且，后面也会合并到主干，感觉有点乱）
 
所以这次，相当于代码，返回到，整合了SSM和Log的配置的代码，重新开始整合SprigSecurity（但是，这次是与数据库打交道，实现权限控制）

> 注意：每个分支是对应的代码，主干则是糅合了每部分代码，请，自行切换分支 

分支：

# 2019_09_14start(01)：  初始化，拉取的项目代码，可看此处(其实就是，一开始起步的代码，SpringBoot整合了SSM以及@Slf4J)  

# 2019_09_14security(01): 整合SpringSecurity现在只到----->配置拦截策略

#  2019_09_17securoty(2)：算是，与数据库成功打交道了
> 需要注意的是：进行到这一步，那么，自己数据库的用户表里面的密码  一定需要加密形式（你是用什么加密方式保存的，那么自动装换就是了）保存

  如下图，密码，自己转化为了admin  和  user

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927115823801.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)


说明：
自己这里，并没有设置退出的步骤，所以，一开始登录了admin的操作，那么，你会发现无论输入http://localhost:8080/security/admin  还是http://localhost:8080/security/user
  都是可以访问的  因为自己数据库是分配了权限的

那么，你如果想看user的操作 （这里是 ，不可看admin页面的内容的）   那么，你要么直接关掉该页面     要么，重开浏览器进行（1）使用user账号登录    （2）输入网址http://localhost:8080/security/admin   你会发现报错

# 2019_09_17securoty(2) 结果：
http://localhost:8080/security/user
会自动跳到对应的登录页

>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120223590.png)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120236855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120114969.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120250235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120304143.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120311684.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120317440.png)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120324760.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190927120331350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)



## Sql：

### 2019_09_14security(01): 结果
运行项目，输入http://localhost:8080/security/login跳转到的页面就是我们刚才写好的页面了，随便输入账号密码点击登录的报错页面也是刚刚添加的error页面。

因为控制层，已经有了方法，会跳转到哪里，至于为什么一直会跳转到error页面，这里还未做  任何  认证以及鉴证的处理。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190917002352666.png)

上面忽略方法，见SecurityConfig配置类，注解有说


此时再运行项目，输入http://localhost:8080/security/login跳转到的页面就是我们刚才写好的页面了，随便输入账号密码点击登录的报错页面也是刚刚添加的error页面。
因为控制层，已经有了方法，会跳转到哪里，至于为什么一直会跳转到error页面，这里还未做  任何  认证以及鉴证的处理。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190917002507616.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190917002619359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190917002624670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)


### CREATE TABLE `security_user` (
 
 `id` varchar(250) NOT NULL COMMENT 'id',
 
 `username` varchar(60) DEFAULT NULL COMMENT '用户名',
 
 `password` varchar(60) DEFAULT NULL COMMENT '密码',
 
 `created_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
 
 `updated_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
 
 PRIMARY KEY (`id`),
 
 UNIQUE KEY `UNIQUE` (`username`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='整合SpringSecurity的用户表'

![数据](https://img-blog.csdnimg.cn/20190917001127291.png)

### CREATE TABLE `security_role` (

  `id` varchar(255) NOT NULL COMMENT 'id',
  
  `name` varchar(60) DEFAULT NULL COMMENT '权限名',
  
  `created_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  
  PRIMARY KEY (`id`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='整合SpringSecurity所需的 角色表'

![角色数据](https://img-blog.csdnimg.cn/20190917001232813.png)

### CREATE TABLE `security_user_role` (

  `id` varchar(250) CHARACTER SET utf8 NOT NULL COMMENT 'id',
  
  `user_id` varchar(250) CHARACTER SET utf8 DEFAULT NULL COMMENT '用户表id',
  
  `role_id` varchar(250) CHARACTER SET utf8 DEFAULT NULL COMMENT '权限表id',
  
  `created_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  
  PRIMARY KEY (`id`),
  
  KEY `user_id` (`user_id`),
  
  KEY `role_id` (`role_id`),
  
  CONSTRAINT `security_user_role_ibfk_1` FOREIGN KEY (`user_id`) REFERENCES `security_user` (`id`),
  
  CONSTRAINT `security_user_role_ibfk_2` FOREIGN KEY (`role_id`) REFERENCES `security_role` (`id`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='整合Security的 用户权限表-->是用户表与权限表的中间表（因为两表是多对多的关系）'

![角色用户中间表数据](https://img-blog.csdnimg.cn/20190917002001410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)

### CREATE TABLE `security_permission` (

  `id` varchar(255) NOT NULL COMMENT 'id',
  
  `name` varchar(30) DEFAULT NULL COMMENT '权限名',
  
  `description` varchar(100) DEFAULT NULL COMMENT '权限说明',
  
  `url` varchar(100) DEFAULT NULL COMMENT '权限允许的URL',
  
  `pid` varchar(255) DEFAULT NULL,
  
  PRIMARY KEY (`id`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='权限表'

![权限表数据](https://img-blog.csdnimg.cn/20190917002104533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)

### CREATE TABLE `security_permission_role` (

  `id` varchar(255) NOT NULL,
  
  `role_id` varchar(255) DEFAULT NULL,
  
  `permission_id` varchar(255) DEFAULT NULL,
  
  PRIMARY KEY (`id`),
  
  KEY `role2` (`role_id`),
  
  KEY `permission` (`permission_id`),
  
  CONSTRAINT `permission` FOREIGN KEY (`permission_id`) REFERENCES `security_permission` (`id`),
  
  CONSTRAINT `role2` FOREIGN KEY (`role_id`) REFERENCES `security_role` (`id`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='权限角色表'

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190917002155690.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lfMjc5NjExNDgw,size_16,color_FFFFFF,t_70)























