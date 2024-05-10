[TOC]

You must change the variable `log_bin_trust_function_creators` to `1` during Ranger installation.

From RDS Dashboard>Parameter group (on the left side of the page):

1. Set the MySQL Server variable `log_bin_trust_function_creators` to `1`.
2. (Optional) After Ranger installation is complete, reset `log_bin_trust_function_creators` to its original setting. The variable is only required to be set to `1` during Ranger installation.

For more information, see:

- [Stratalux: Why You Should Always Use a Custom DB Parameter Group When Creating an RDS Instance](https://www.stratalux.com/blog/always-use-custom-db-parameter-group-creating-rds-instance/)
- [AWS Documentation>Amazon RDS DB Instance Lifecycle » Working with DB Parameter Groups](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithParamGroups.html)
- [MySQL 5.7 Reference Manual >Binary Logging of Stored Programs](https://dev.mysql.com/doc/refman/5.7/en/stored-programs-logging.html)
