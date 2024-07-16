[TOC]

New in version 1.6.0.

Kyuubi administer tool(kyuubi-admin) provides administrators with some maintenance operations against a kyuubi server or cluster.

Installation
--------------------------------------------------------------------------------------------------------------------

To install kyuubi-admin, you need to unpack the tarball. For example,

```shell
tar zxf apache-kyuubi-1.9.1-bin.tgz
```

This will result in the creation of a subdirectory named apache-kyuubi-1.9.1-bin shown below,

```shell
apache-kyuubi-1.9.1-bin
├── ...
├── bin
|   ├── kyuubi-admin
│   ├── ...
├── ...
```

Usage
------------------------------------------------------------------------------------------------------

```shell
bin/kyuubi-admin --help
```

Refresh config
------------------------------------------------------------------------------------------------------------------------

Refresh the config with specified type.

Usage: `bin/kyuubi-admin refresh config [options] [<configType>]`

| Config Type | Description|
| --- | --- |
| hadoopConf| The hadoop conf used for proxy user verification.|
| userDefaultsConf| The user defaults configs with key in format in the form of ___{username}___.{config key} from default property file. |
| unlimitedUsers| The users without maximum connections limitation. |
| denyUsers| The user in the deny list will be denied to connect to kyuubi server. |

List Engines--------------------------------------------------------------------------------------------------------------------

Prints a table of the key information about the specified engines.

Usage: `bin/kyuubi-admin list engine [options]`

| Options | Description|
| --- | --- |
| -et, –engine-type| The engine type. If not specified, it will read the configuration item kyuubi.engine.type from kyuubi-defaults.conf. |
| -esl, –engine-share-level| The engine share level. If not specified, it will read the configuration item kyuubi.engine.share.level from kyuubi-defaults.conf. |
| -es, –engine-subdomain| The subdomain for the share level of an engine. If not specified, it will read the configuration item kyuubi.engine.share.level.subdomain from kyuubi-defaults.conf. |
| –hs2ProxyUser| The proxy user to impersonate. When specified, it will list engines for the hs2ProxyUser. |

List Servers
--------------------------------------------------------------------------------------------------------------------

Prints a table of the key information about the servers.

Usage: `bin/kyuubi-admin list server`

Delete an Engine
----------------------------------------------------------------------------------------------------------------------------

Delete the specified engine.

Usage: `bin/kyuubi-admin delete engine [options]`

| Options| Description |
| --- | --- |
| -et, –engine-type| The engine type. If not specified, it will read the configuration item kyuubi.engine.type from kyuubi-defaults.conf. |
| -esl, –engine-share-level| The engine share level. If not specified, it will read the configuration item kyuubi.engine.share.level from kyuubi-defaults.conf. |
| -es, –engine-subdomain | The subdomain for the share level of an engine. If not specified, it will read the configuration item kyuubi.engine.share.level.subdomain from kyuubi-defaults.conf. Default value is “default”. |
| –hs2ProxyUser| The proxy user to impersonate. When specified, it will delete engines for the hs2ProxyUser. |
