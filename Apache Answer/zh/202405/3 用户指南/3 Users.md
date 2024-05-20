[TOC]

## 用户状态

![User state diagram](https://answer.apache.org/img/docs/users-user-status.drawio.svg)

## 热门用户

显示平台中排名靠前的用户。

- **本周声誉得分最高的用户**
    - 本周声誉增加最多的用户
    - 显示声誉提高的前 20 位用户（按顺序）
- **本周投票最多的用户**
    - 投票给其他人的票数
    - 显示前 20 位用户及其投票数（按顺序）
- **我们的社区工作人员**
    - 显示所有版主、管理员
    - 按信誉排序

## 注册

使用电子邮件进行用户注册过程。

![Sign up process](https://answer.apache.org/img/docs/users-signup.drawio.svg)

- 显示名称（缩写为“名称”）：
    - 少于 30 个字符。
- 用户名：
    - 独特的。
    - 少于 30 个字符。
    - 只能包含 `0-9`、小写字母 `a-z`、符号 `- 。 _`。
    - 根据显示名称生成，空格用符号“-”替换。
    - 如果有重复，则在末尾添加 4 个随机字符，例如`乔-x7k2`。
    - 不允许保留关键字。
- 记录注册时间和IP地址。
- 激活链接的有效期为 14 天。

## 登录

用户想要登录，用户的登录权限与状态相关。

|用户状态 |正常 |不活跃 |暂停 |已删除 |
|---|---|---|---|---|
|登录 |允许 |被拒绝 |被拒绝 |被拒绝 |

### 使用电子邮件和密码登录

- 填写电子邮件和密码进行登录。
    - 如果用户不存在，则显示“无效的电子邮件或密码”消息，以防止帐户被攻击。
    - 当非活动用户登录时，转到要求激活的页面。
    - 当被暂停的用户登录时，进入禁止提示页面。
- 默认情况下，登录状态会被记住 14 天。
- 如果有人忘记密码，请单击“忘记密码”来重置密码。

### 从第三方OAuth登录

![Thirdy-party OAuth process](https://answer.apache.org/img/docs/users-oauth.drawio.svg)

## Reset password

TODO

## Notification

TODO

### Inbox

TODO

### Achievement

TODO

## Profile

TODO

## Settings

TODO

### Unsubscribe email

TODO

