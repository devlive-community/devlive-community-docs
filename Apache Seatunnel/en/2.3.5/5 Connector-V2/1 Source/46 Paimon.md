[TOC]

> Paimon source connector

## Description

Read data from Apache Paimon.

## Key features

- [x] [batch]($Intro-To-Connector-V2-Features)
- [ ] [stream]($Intro-To-Connector-V2-Features)
- [ ] [exactly-once]($Intro-To-Connector-V2-Features)
- [ ] [column projection]($Intro-To-Connector-V2-Features)
- [ ] [parallelism]($Intro-To-Connector-V2-Features)
- [ ] [support user-defined split]($Intro-To-Connector-V2-Features)

## Options

|      name      |  type  | required | default value |
|----------------|--------|----------|---------------|
| warehouse      | String | Yes      | -             |
| database       | String | Yes      | -             |
| table          | String | Yes      | -             |
| hdfs_site_path | String | No       | -             |

### warehouse [string]

Paimon warehouse path

### database [string]

The database you want to access

### table [string]

The table you want to access

### hdfs_site_path [string]

The file path of `hdfs-site.xml`

## Examples

```hocon
source {
 Paimon {
     warehouse = "/tmp/paimon"
     database = "default"
     table = "st_test"
   }
}
```

## Changelog

### next version

- Add Paimon Source Connector

