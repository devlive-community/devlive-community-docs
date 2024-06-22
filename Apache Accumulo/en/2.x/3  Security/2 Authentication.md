[TOC]

Accumulo has authentication to verify the identity of users.

Configuration
-------------------------------------------------------------------------------------------

Accumulo can be configured to use different authentication methods:

| Method                 | Setting for [instance.security.authenticator]($Server-Properties-2.x#instance_security_authenticator)                                                                                                                                     |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password **(default)** | [org.apache.accumulo.server.security.handler.ZKAuthenticator](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/ZKAuthenticator.html)             |
| [Kerberos]($Kerberos)          | [org.apache.accumulo.server.security.handler.KerberosAuthenticator](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/KerberosAuthenticator.html) |

All authentication methods implement [Authenticator](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/Authenticator.html). The default (password-based) implementation method is described in this document.

Root user
-----------------------------------------------------------------------------------

When [Accumulo is initialized]($Setup#initialization), a `root` user is created and given a password. This `root` user is used to create other users.

Creating users
---------------------------------------------------------------------------------------------

Users can be created in the shell:

```
root@uno> createuser bob
Enter new password for 'bob': ****
Please confirm new password for 'bob': ****
```

In the Java API using [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html):

```
client.securityOperations().createLocalUser("bob", new PasswordToken("pass"));
```

Authenticating users
---------------------------------------------------------------------------------------------------------

Users are authenticated when they [create an Accumulo client]($Accumulo-Clients#creating-an-accumulo-client) or when they log in to the [Accumulo shell](https://accumulo.apache.org/docs/2.x/getting-started/shell).

Authentication can also be tested in the shell:

```
root@myinstance mytable> authenticate bob
Enter current password for 'bob': ****
Valid
```

In the Java API using [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html):

```
boolean valid = client.securityOperations().authenticateUser("bob", new PasswordToken("pass"));
```

Changing user passwords
---------------------------------------------------------------------------------------------------------------

A user’s password can be changed in the shell:

```
root@uno> passwd -u bob
Enter current password for 'root': ******
Enter new password for 'bob': ***
```

In the Java API using [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html):

```
client.securityOperations().changeLocalUserPassword("bob", new PasswordToken("pass"));
```

Removing users
---------------------------------------------------------------------------------------------

Users can be removed in the shell:

```
root@uno> dropuser bob
dropuser { bob } (yes|no)? yes
```

In the Java API using [SecurityOperations](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/admin/SecurityOperations.html):

```
client.securityOperations().dropLocalUser("bob");
```
