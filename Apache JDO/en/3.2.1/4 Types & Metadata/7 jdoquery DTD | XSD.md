[TOC]

JDO defines XML MetaData in **jdo** files as well as **orm** files, but also specifies that named queries can be defined in *jdoquery* files. As always with XML, the metadata must match the defined DTD/XSD for that file type. This section describes the content of the **jdoquery** files. All **jdoquery** files must contain a valid DTD/DOCTYPE specification. You can use PUBLIC or SYSTEM versions of these.

Here are a few examples valid for **jdoquery** files eith DTD specification

```xml
<!DOCTYPE jdoquery PUBLIC
    "-//The Apache Software Foundation//DTD Java Data Objects Query Metadata 3.2//EN"
    "https://db.apache.org/jdo/xmlns/jdoquery\_3\_2.dtd">
```

or

```xml
<!DOCTYPE jdoquery SYSTEM "file:/javax/jdo/jdoquery.dtd">
```

Here is an example valid for **jdoquery** files with XSD specification

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<jdoquery xmlns="https://db.apache.org/jdo/xmlns/jdoquery"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://db.apache.org/jdo/xmlns/jdoquery https://db.apache.org/jdo/xmlns/jdoquery\_3\_2.xsd" version="3.2">
    ...
</jdoquery>
```

Your MetaData should match either the [DTD](https://db.apache.org/jdo/xmlns/jdoquery_3_2.dtd) or the [XSD](https://db.apache.org/jdo/xmlns/jdoquery_3_2.xsd) specification.
