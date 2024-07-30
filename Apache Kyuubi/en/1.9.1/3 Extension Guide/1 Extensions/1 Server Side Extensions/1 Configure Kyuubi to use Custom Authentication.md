[TOC]

Besides the [builtin authentication]($Authentication) methods, kyuubi supports custom authentication implementations of `org.apache.kyuubi.service.authentication.PasswdAuthenticationProvider`.

```java
package org.apache.kyuubi.service.authentication

import javax.security.sasl.AuthenticationException

trait PasswdAuthenticationProvider {

  /**
   * The authenticate method is called by the Kyuubi Server authentication layer
   * to authenticate users for their requests.
   * If a user is to be granted, return nothing/throw nothing.
   * When a user is to be disallowed, throw an appropriate [[AuthenticationException]].
   *
   * @param user     The username received over the connection request
   * @param password The password received over the connection request
   *
   * @throws AuthenticationException When a user is found to be invalid by the implementation
   */
  @throws[AuthenticationException]
  def authenticate(user: String, password: String): Unit
}
```

Build A Custom Authenticator
------------------------------------------------------------------------------------------------------------------------------------------------------------------

To create custom Authenticator class derived from the above interface, we need to:

*   Referencing the library

```xml
<dependency>
   <groupId>org.apache.kyuubi</groupId>
   <artifactId>kyuubi-common\_2.12</artifactId>
   <version>1.9.1</version>
   <scope>provided</scope>
</dependency>
```

*   Implement PasswdAuthenticationProvider - [Sample Code](https://github.com/kyuubilab/example-custom-authentication/blob/main/src/main/scala/org/apache/kyuubi/example/MyAuthenticationProvider.scala)

Enable Custom Authentication
------------------------------------------------------------------------------------------------------------------------------------------------------------------

To enable the custom authentication method, we need to

*   Put the jar package to `$KYUUBI_HOME/jars` directory to make it visible for the classpath of the kyuubi server.
*   Configure the following properties to `$KYUUBI_HOME/conf/kyuubi-defaults.conf` on each node where kyuubi server is installed.

```java
kyuubi.authentication=CUSTOM
kyuubi.authentication.custom.class=YourAuthenticationProvider
```

*   Restart all the kyuubi server instances
