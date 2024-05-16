[TOC]

n9e-webapi 模块提供了两类接口，一个是 `/api/n9e` 打头的，给前端调用，另一类是 `/v1/n9e` 打头的，给第三方系统调用。如果想以个人身份模仿WEB操作，也是调用 `/api/n9e` 相关接口。

以个人身份模仿WEB操作
------------

这种方式，页面上 JavaScript 可以调用的所有接口，你都可以用程序调用，打开 chrome 的开发者工具，扒拉这些接口，还是非常容易的。当然，要先登录，登录调用 webapi 模块的 `/api/n9e/auth/login` 接口，系统使用 jwt 认证，如果登录成功，会返回 access\_token 和 refresh\_token，每次调用的时候都要把 access\_token 放到 Header 里，access\_token 差不多15分钟过期，之后可以重新调用登录接口换 token，也可以调用 `/api/n9e/auth/refresh` 接口用 refresh\_token 换一个新的 access\_token，当然，也会顺道返回一个新的 refresh\_token，举例：

    # 调用登录接口拿到access_token和refresh_token记录下来，后面调用其他接口的时候会用到
    [root@10-255-0-34 ~]# curl -X POST 'http://localhost:18000/api/n9e/auth/login' -d '{"username": "root", "password": "root.2020"}'
    {"dat":{"access_token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhY2Nlc3NfdXVpZCI6ImIxNTcyMjgwLWZlNzAtNDhjZi1hNDQ3LWVlMjVhZmYwMjRhZCIsImF1dGhvcml6ZWQiOnRydWUsImV4cCI6MTYzNzgyMzA1OSwidXNlcl9pZGVudGl0eSI6IjEtcm9vdCJ9.nJ56Pc7qS5Ik_UaVmlNWu_QlABaBc4pZ_WkU45u2wWk","refresh_token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MzgzMzc4NTksInJlZnJlc2hfdXVpZCI6ImIxNTcyMjgwLWZlNzAtNDhjZi1hNDQ3LWVlMjVhZmYwMjRhZCsrMS1yb290IiwidXNlcl9pZGVudGl0eSI6IjEtcm9vdCJ9.JKsbfTYBCOOfR_oPsf496N9ml9yXbP7BHb4E8Yfnzbo","user":{"id":1,"username":"root","nickname":"超管","phone":"","email":"","portrait":"","roles":["Admin"],"contacts":{},"create_at":1637545881,"create_by":"system","update_at":1637546351,"update_by":"root","admin":true}},"err":""}
    
    # access_token放到Authorization这个Header里，Bearer的验证方式
    [root@10-255-0-34 ~]# curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhY2Nlc3NfdXVpZCI6ImIxNTcyMjgwLWZlNzAtNDhjZi1hNDQ3LWVlMjVhZmYwMjRhZCIsImF1dGhvcml6ZWQiOnRydWUsImV4cCI6MTYzNzgyMzA1OSwidXNlcl9pZGVudGl0eSI6IjEtcm9vdCJ9.nJ56Pc7qS5Ik_UaVmlNWu_QlABaBc4pZ_WkU45u2wWk" 'http://localhost:18000/api/n9e/self/profile'
    {"dat":{"id":1,"username":"root","nickname":"超管","phone":"","email":"","portrait":"","roles":["Admin"],"contacts":{},"create_at":1637545881,"create_by":"system","update_at":1637546351,"update_by":"root","admin":true},"err":""}
    
    # 如果token过期了，后端会返回异常HTTP状态码，此时要调用refresh接口换取新的token
    [root@10-255-0-34 ~]# curl -X POST 'http://localhost:18000/api/n9e/auth/refresh' -d '{"refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MzgzMzc4NTksInJlZnJlc2hfdXVpZCI6ImIxNTcyMjgwLWZlNzAtNDhjZi1hNDQ3LWVlMjVhZmYwMjRhZCsrMS1yb290IiwidXNlcl9pZGVudGl0eSI6IjEtcm9vdCJ9.JKsbfTYBCOOfR_oPsf496N9ml9yXbP7BHb4E8Yfnzbo"}'
    {"dat":{"access_token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhY2Nlc3NfdXVpZCI6IjAxMzkzYzkxLTk5MWItNGE0Yi04ODk2LTJhZGRjMDUwYjcxMCIsImF1dGhvcml6ZWQiOnRydWUsImV4cCI6MTYzNzgyMzMxOCwidXNlcl9pZGVudGl0eSI6IjEtcm9vdCJ9.2BeWyYfcnRi3qw69zecaaeFnPFUNAGsiPIZBBnd5lug","refresh_token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MzgzMzgxMTgsInJlZnJlc2hfdXVpZCI6IjAxMzkzYzkxLTk5MWItNGE0Yi04ODk2LTJhZGRjMDUwYjcxMCsrMS1yb290IiwidXNlcl9pZGVudGl0eSI6IjEtcm9vdCJ9.zFZaRYcJI6G5maSgDVF-jZzxQ3Tb5dybIqufJhBy034"},"err":""}


第三方系统调用夜莺
---------

比如第三方系统想获取夜莺中的所有未恢复告警，或者获取夜莺中的全量用户列表，这些需求，建议走 `/v1/n9e` 打头的接口，这些接口走 BasicAuth 认证，BasicAuth 的用户名和密码在 webapi.conf 中可以找到，就是 BasicAuth 那个 section 的配置。当前这个阶段，`/v1/n9e` 前缀的接口还比较少，不过代码框架已经搭起来了，代码在 `src/webapi/router/router.go` 文件中，如果贵司要封装夜莺的接口，可能要在这个路由分组下加一些路由配置了，欢迎大家 PR。
