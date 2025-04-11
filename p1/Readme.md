<https://www.yuque.com/chengxuyuancarl/px6ppg/bg81521ec7570q18#WO4X2>
<https://github.com/youngyangyang04/kamanotes>
# kamanotes

这是一个关于笔记分享的项目
前端应用层：
* 登录注册
* 笔记管理
* 个人中心

API网管层
Spring Securiyt + JWT认证
业务服务层
* 用户注册
* 验证码管理
* 个人信息维护
* 笔记维护
* makedown笔记
* 点赞，分享系统
* 搜索服务
* 全文搜索
* 结果缓存

数据访问层
* mysql
* redis nosql存文档
* 文件存储

# 数据流向
* 用户请求
* Spring Security过滤器
* Jwt token 验证
* ThreadLocal用户上下文
* controller接口
* mybatis数据访问
* Mysql/redis存储

> 关于JWt token验证
> JSON Web Token（缩写 JWT）是目前最流行的跨域认证解决方案
> 详见关于jwt

## 关于redis缓存
验证码String 15m
搜索String 30m
排行Zset 实时更新
计数器Hash 定时同步 ？什么是计数器

# API文档
所有API请求基础路径：
localhost:8080/api

### 1.使用JWT token进行认证
在请求头中添加Authorization: Bearer<token>
响应格式：
```
code:200
message:成功
data:#响应数据
token:"xxx" //JWT token
```

### 2.用户相关接口
restful的几种http方法
* get获取资源
* head与get类似，但不返回body内容
* post创建子资源
* put创建，更新资源
* delete删除资源
* optionsurl验证检测
* patch创建更新部分资源

*用户注册*
请求路径: post /api/users
请求参数：
```
account:string
username:string
password:string
email:string
verifyCode:string 验证码
```
响应参数：
```
code:200
message:success
data:
  userId
  account
  username
  email
  emailVerified
token:
```

*用户登录*
路径 Post /api/users/login
请求
```
account
email
password
```

响应：
```
code
message
data
  //关于用户的信息
token
```

*发送验证码*
Get /api/email/verify-code

发送
```
email:
type: register,reset_passWord
```

响应
```
code:200
message:success
data:
```

*获取当前用户信息*
post /api/users/whoiam
请求头:需要Jwt token
