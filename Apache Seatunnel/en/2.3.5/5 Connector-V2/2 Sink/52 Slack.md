[TOC]

> Slack sink connector

## Support Those Engines

> Spark<br/>
> Flink<br/>
> SeaTunnel Zeta<br/>

## Key features

- [ ] [exactly-once]($Intro-To-Connector-V2-Features)
- [ ] [cdc]($Intro-To-Connector-V2-Features)

## Description

Used to send data to Slack Channel. Both support streaming and batch mode.

> For example, if the data from upstream is [`age: 12, name: huan`], the content send to socket server is the following: `{"name":"huan","age":17}`

## Data Type Mapping

All data types are mapped to string.

## Options

|      Name      |  Type  | Required | Default |                                             Description                                             |
|----------------|--------|----------|---------|-----------------------------------------------------------------------------------------------------|
| webhooks_url   | String | Yes      | -       | Slack webhook url                                                                                   |
| oauth_token    | String | Yes      | -       | Slack oauth token used for the actual authentication                                                |
| slack_channel  | String | Yes      | -       | slack channel for data write                                                                        |
| common-options |        | no       | -       | Sink plugin common parameters, please refer to [Sink Common Options]($SK-Sink-Common-Options) for details |

## Task Example

### Simple:

```hocon
sink {
 SlackSink {
  webhooks_url = "https://hooks.slack.com/services/xxxxxxxxxxxx/xxxxxxxxxxxx/xxxxxxxxxxxxxxxx"
  oauth_token = "xoxp-xxxxxxxxxx-xxxxxxxx-xxxxxxxxx-xxxxxxxxxxx"
  slack_channel = "channel name"
 }
}
```

## Changelog

### new version

- Add Slack Sink Connector

