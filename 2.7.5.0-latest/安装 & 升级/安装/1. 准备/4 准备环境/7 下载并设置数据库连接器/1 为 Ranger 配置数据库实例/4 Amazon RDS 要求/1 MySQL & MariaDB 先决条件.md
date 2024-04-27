您必须在 Ranger 安装期间将变量 `log_bin_trust_function_creators` 更改为 `1`。

从 RDS 仪表板 > 参数组（位于页面左侧）：

1. 将 MySQL 服务器变量 `log_bin_trust_function_creators` 设置为 `1`。
2. (可选) Ranger 安装完成后，将 `log_bin_trust_function_creators` 重置为其原始设置。该变量只需在 Ranger 安装期间设置为 `1` 即可。

有关更多信息，请参阅：

- [Stratalux：为什么在创建 RDS 实例时应始终使用自定义数据库参数组](https://www.stratalux.com/blog/always-use-custom-db-parameter-group-creating-rds-instance/)
- [AWS 文档 > Amazon RDS 数据库实例生命周期 » 使用数据库参数组](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithParamGroups.html)
- [MySQL 5.7 参考手册 > 存储程序的二进制日志记录](https://dev.mysql.com/doc/refman/5.7/en/stored-programs-logging.html)
