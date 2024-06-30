[TOC]

## JDBC Catalog

Iceberg supports using a table in a relational database to manage Iceberg tables through JDBC.
The database that JDBC connects to must support atomic transaction to allow the JDBC catalog implementation to
properly support atomic Iceberg table commits and read serializable isolation.

### Configurations

Because each database and database service provider might require different configurations,
the JDBC catalog allows arbitrary configurations through:

| Property             | Default                           | Description                                            |
| -------------------- | --------------------------------- | ------------------------------------------------------ |
| uri                  |                                   | the JDBC connection string |
| jdbc.<property_key\> |                                   | any key value pairs to configure the JDBC connection | 

### Examples


#### Spark

You can start a Spark session with a MySQL JDBC connection using the following configurations:

```shell
spark-sql --packages org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:{{ icebergVersion }} \
    --conf spark.sql.catalog.my_catalog=org.apache.iceberg.spark.SparkCatalog \
    --conf spark.sql.catalog.my_catalog.warehouse=s3://my-bucket/my/key/prefix \
    --conf spark.sql.catalog.my_catalog.type=jdbc \
    --conf spark.sql.catalog.my_catalog.uri=jdbc:mysql://test.1234567890.us-west-2.rds.amazonaws.com:3306/default \
    --conf spark.sql.catalog.my_catalog.jdbc.verifyServerCertificate=true \
    --conf spark.sql.catalog.my_catalog.jdbc.useSSL=true \
    --conf spark.sql.catalog.my_catalog.jdbc.user=admin \
    --conf spark.sql.catalog.my_catalog.jdbc.password=pass
```

#### Java API

```java
Class.forName("com.mysql.cj.jdbc.Driver"); // ensure JDBC driver is at runtime classpath
Map<String, String> properties = new HashMap<>();
properties.put(CatalogProperties.CATALOG_IMPL, JdbcCatalog.class.getName());
properties.put(CatalogProperties.URI, "jdbc:mysql://localhost:3306/test");
properties.put(JdbcCatalog.PROPERTY_PREFIX + "user", "admin");
properties.put(JdbcCatalog.PROPERTY_PREFIX + "password", "pass");
properties.put(CatalogProperties.WAREHOUSE_LOCATION, "s3://warehouse/path");
Configuration hadoopConf = new Configuration(); // configs if you use HadoopFileIO
JdbcCatalog catalog = CatalogUtil.buildIcebergCatalog("test_jdbc_catalog", properties, hadoopConf);
```
