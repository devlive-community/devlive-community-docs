[TOC]

> New in version 1.5.0.

Session Conf Advisor
-------------------------------------------------------------------------------------------------------------------------------------------------

Kyuubi supports inject session configs with custom config advisor. It is usually used to append or overwrite session configs dynamically, so administrators of Kyuubi can have an ability to control the user specified configs.

The steps of injecting session configs
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1.  create a custom class which implements the `org.apache.kyuubi.plugin.SessionConfAdvisor`.
2.  compile and put the jar into `$KYUUBI_HOME/jars`
3.  adding configuration at `kyuubi-defaults.conf`:

    ```java
    kyuubi.session.conf.advisor=${classname}
    ```

The `org.apache.kyuubi.plugin.SessionConfAdvisor` has a zero-arg constructor, holds one method with user and session conf and returns a new conf map.

```java
public interface SessionConfAdvisor {
  default Map<String, String> getConfOverlay(String user, Map<String, String> sessionConf) {
    return Collections.EMPTY_MAP;
  }
}
```

> The returned conf map will overwrite the original session conf.

Example
-----------------------------------------------------------------------------------------------------------------------

We have a custom class `CustomSessionConfAdvisor`:

```java
public class CustomSessionConfAdvisor implements SessionConfAdvisor {
  @Override
  Map<String, String> getConfOverlay(String user, Map<String, String> sessionConf) {
    if ("uly".equals(user)) {
      return Collections.singletonMap("spark.driver.memory", "1G");
    } else {
      return Collections.EMPTY_MAP;
    }
  }
}
```

If a user uly creates a connection with:

```java
jdbc:hive2://localhost:10009/;hive.server2.proxy.user=uly;#spark.driver.memory=2G
```

The final Spark application will allocate `1G` rather than `2G` for the driver jvm.
