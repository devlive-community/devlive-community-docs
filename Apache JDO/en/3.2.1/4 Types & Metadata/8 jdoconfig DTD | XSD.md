[TOC]

## Meta-Data - JDOConfig

JDO allows you to define a file *jdoconfig.xml* that specifies the properties for a named PMF. As always with XML, the metadata must match the defined DTD/XSD for that file type. This section describes the content of the **jdoconfig** files. All **jdoconfig** files must contain a valid DTD/DOCTYPE specification. You can use PUBLIC or SYSTEM versions of these.

Here are a few examples valid for **jdoconfig** files with DTD specifications

```xml
<!DOCTYPE jdoconfig PUBLIC
    "-//The Apache Software Foundation//DTD Java Data Objects Configuration 3.2//EN"
    "https://db.apache.org/jdo/xmlns/jdoconfig\_3\_2.dtd">

<!DOCTYPE jdoconfig SYSTEM "file:/javax/jdo/jdoconfig.dtd">
```

Here is an example valid for **jdoconfig** files with XSD specification

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<jdoconfig xmlns="https://db.apache.org/jdo/xmlns/jdoconfig"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://db.apache.org/jdo/xmlns/jdoconfig https://db.apache.org/jdo/xmlns/jdoconfig\_3\_2.xsd" version="3.2">
    ...
</jdoconfig>
```

Your MetaData should match either the [DTD](https://db.apache.org/jdo/xmlns/jdoconfig_3_2.dtd) or the [XSD](https://db.apache.org/jdo/xmlns/jdoconfig_3_2.xsd) specification.
