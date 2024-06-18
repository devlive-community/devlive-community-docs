[TOC]

> TDengine source connector

## Description

Read external data source data through TDengine.

## Key features

- [x] [batch]($Intro-To-Connector-V2-Features)
- [ ] [stream]($Intro-To-Connector-V2-Features)
- [x] [exactly-once]($Intro-To-Connector-V2-Features)
- [ ] [column projection]($Intro-To-Connector-V2-Features)

supports query SQL and can achieve projection effect.

- [x] [parallelism]($Intro-To-Connector-V2-Features)
- [ ] [support user-defined split]($Intro-To-Connector-V2-Features)

## Options

|    name     |  type  | required | default value |
|-------------|--------|----------|---------------|
| url         | string | yes      | -             |
| username    | string | yes      | -             |
| password    | string | yes      | -             |
| database    | string | yes      |               |
| stable      | string | yes      | -             |
| lower_bound | long   | yes      | -             |
| upper_bound | long   | yes      | -             |

### url [string]

the url of the TDengine when you select the TDengine

e.g.

```
jdbc:TAOS-RS://localhost:6041/
```

### username [string]

the username of the TDengine when you select

### password [string]

the password of the TDengine when you select

### database [string]

the database of the TDengine when you select

### stable [string]

the stable of the TDengine when you select

### lower_bound [long]

the lower_bound of the migration period

### upper_bound [long]

the upper_bound of the migration period

## Example

### source

```hocon
source {
        TDengine {
          url : "jdbc:TAOS-RS://localhost:6041/"
          username : "root"
          password : "taosdata"
          database : "power"
          stable : "meters"
          lower_bound : "2018-10-03 14:38:05.000"
          upper_bound : "2018-10-03 14:38:16.800"
          result_table_name = "tdengine_result"
        }
}
```

