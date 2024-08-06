[TOC]

Kyuubi provide event processing mechanism, it can help us to record some events. Beside the builtin `JsonLoggingEventHandler`, Kyuubi supports custom event handler. It is usually used to write Kyuubi events to some external systems. For example, Kafka, ElasticSearch, etc. The `org.apache.kyuubi.events.handler.CustomEventHandlerProvider` has a zero-arg constructor, it can help us to create a custom EventHandler.

```java
package org.apache.kyuubi.events.handler

import org.apache.kyuubi.config.KyuubiConf
import org.apache.kyuubi.events.KyuubiEvent

/**
 * Custom EventHandler provider. We can implement it to provide a custom EventHandler.
 * The implementation will be loaded by ``Service Provider Interface``.
 */
trait CustomEventHandlerProvider {

  /**
   * The create method is called to create a custom event handler
   * when this implementation is loaded.
   *
   * @param kyuubiConf The conf can be used to read some configs.
   * @return A custom handler to handle KyuubiEvent.
   */
   def create(kyuubiConf: KyuubiConf): EventHandler[KyuubiEvent]
}
```

Build A Custom EventHandler
--------------------------------------------------------------------------------------------------------------------------------------------------------

To create custom EventHandlerProvider class derived from the above interface, we need to:

*   Referencing the library

```xml
<dependency>
    <groupId>org.apache.kyuubi</groupId>
    <artifactId>kyuubi-events_2.12</artifactId>
    <version>1.9.1</version>
    <scope>provided</scope>
</dependency>
```

*   Implement `org.apache.kyuubi.events.handler.CustomEventHandlerProvider`
*   Adding a file named `org.apache.kyuubi.events.handler.CustomEventHandlerProvider` in the src/main/resources/META-INF/services folder of project, its content is the custom class name.

Enable Custom EventHandler
------------------------------------------------------------------------------------------------------------------------------------------------------

To enable the custom EventHandler, we need to

*   Put the jar package to `$KYUUBI_HOME/jars` directory to make it visible for the classpath of the kyuubi server.
*   Configure the following properties to `$KYUUBI_HOME/conf/kyuubi-defaults.conf` on each node where kyuubi server is installed. If you need use other event handler, it can be appended after the `CUSTOM`.

```java
kyuubi.backend.server.event.loggers=CUSTOM
```

*   Restart all the kyuubi server instances.
