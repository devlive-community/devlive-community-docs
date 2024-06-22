[TOC]

Accumulo users can only perform actions if they are given permission.

Accumulo has three types of permissions:

*   [SystemPermission](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/security/SystemPermission.html)
*   [NamespacePermission](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/security/NamespacePermission.html)
*   [TablePermission](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/security/TablePermission.html)

These permissions are managed by [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html) in Java API or the [Accumulo shell](https://accumulo.apache.org/docs/2.x/getting-started/shell).

Configuration
----------------------------------------------------------------------------------------

Accumulo’s [PermissionHandler](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/PermissionHandler.html) is configured by setting [instance.security.permissionHandler](https://accumulo.apache.org/docs/2.x/configuration/server-properties#instance_security_permissionHandler).

The default permission handler is described below.

Granting permission
----------------------------------------------------------------------------------------------------

Users can be granted permissions in the shell:

```
root@uno> grant System.CREATE_TABLE -s -u bob
```

Or in the Java API using [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html):

```
client.securityOperations().grantSystem("bob", SystemPermission.CREATE_TABLE);
```

View permissions
----------------------------------------------------------------------------------------------

Permissions can be listed for a user in the shell:

```
root@uno> userpermissions -u bob
System permissions: System.CREATE_TABLE, System.DROP_TABLE

Namespace permissions (accumulo): Namespace.READ

Table permissions (accumulo.metadata): Table.READ
Table permissions (accumulo.replication): Table.READ
Table permissions (accumulo.root): Table.READ
```

Revoking permissions
------------------------------------------------------------------------------------------------------

Permissions can be revoked for a user in the shell

```
root@uno> revoke System.CREATE_TABLE -s -u bob
```

Or in the Java API using [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html):

```
client.securityOperations().revokeSystemPermission("bob", SystemPermission.CREATE_TABLE);
```
