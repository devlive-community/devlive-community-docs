[TOC]

JDO defines XML MetaData in **jdo** files as well as **orm** files. As always with XML, the metadata must match the defined DTD/XSD for that file type. This section describes the content of the **orm** files. The content of **jdo** files can be found [here]($jdo-DTD-XSD). All **orm** files must contain a valid DTD/DOCTYPE specification. You can use PUBLIC or SYSTEM versions of these.

Here are a couple of examples valid for **orm** files with DTD specification

```xml
<!DOCTYPE orm PUBLIC
    "-//The Apache Software Foundation//DTD Java Data Objects Mapping Metadata 3.2//EN"
    "https://db.apache.org/jdo/xmlns/orm\_3\_2.dtd">
```

or

```xml
<!DOCTYPE orm SYSTEM "file:/javax/jdo/orm.dtd">
```

Here is an example valid for **orm** files with XSD specification

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<orm xmlns="https://db.apache.org/jdo/xmlns/orm"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://db.apache.org/jdo/xmlns/orm https://db.apache.org/jdo/xmlns/orm\_3\_2.xsd" version="3.2">
    ...
</orm>
```

Your MetaData should match either the [DTD](https://db.apache.org/jdo/xmlns/orm_3_2.dtd) or the [XSD](https://db.apache.org/jdo/xmlns/orm_3_2.xsd) specification.
