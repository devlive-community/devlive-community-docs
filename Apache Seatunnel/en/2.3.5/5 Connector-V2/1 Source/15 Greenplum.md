# Greenplum

> Greenplum source connector

## Description

Read Greenplum data through [Jdbc connector]($JDBC).

## Key features

- [x] [batch]($Intro-To-Connector-V2-Features)
- [ ] [stream]($Intro-To-Connector-V2-Features)
- [ ] [exactly-once]($Intro-To-Connector-V2-Features)
- [x] [column projection]($Intro-To-Connector-V2-Features)

supports query SQL and can achieve projection effect.

- [x] [parallelism]($Intro-To-Connector-V2-Features)
- [ ] [support user-defined split]($Intro-To-Connector-V2-Features)

> Optional jdbc drivers:
> - `org.postgresql.Driver`
> - `com.pivotal.jdbc.GreenplumDriver`
>
> Warn: for license compliance, if you use `GreenplumDriver` the have to provide Greenplum JDBC driver yourself, e.g. copy greenplum-xxx.jar to $SEATNUNNEL_HOME/lib for Standalone.

## Options

### common options

Source plugin common parameters, please refer to [Source Common Options]($Source-Common-Options) for details.

## Changelog

### 2.2.0-beta 2022-09-26

- Add Greenplum Source Connector

