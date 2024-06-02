[TOC]

[![Image 1: License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![Image 2: GitHub release (latest SemVer)](https://img.shields.io/github/v/release/apache/superset?sort=semver)](https://github.com/apache/superset/tree/latest) [![Image 3: Build Status](https://github.com/apache/superset/workflows/Python/badge.svg)](https://github.com/apache/superset/actions) [![Image 4: PyPI version](https://badge.fury.io/py/apache-superset.svg)](https://badge.fury.io/py/apache-superset) [![Image 5: Coverage Status](https://codecov.io/github/apache/superset/coverage.svg?branch=master)](https://codecov.io/github/apache/superset) [![Image 6: PyPI](https://img.shields.io/pypi/pyversions/apache-superset.svg?maxAge=2592000)](https://pypi.python.org/pypi/apache-superset) [![Image 7: Get on Slack](https://img.shields.io/badge/slack-join-orange.svg)](http://bit.ly/join-superset-slack) [![Image 8: Documentation](https://img.shields.io/badge/docs-apache.org-blue.svg)](https://superset.apache.org/)

![Image 9: Superset logo (light)](https://superset.apache.org/img/superset-logo-horiz-apache.svg)A modern, enterprise-ready business intelligence web application.

[**Why Superset?**](#why-superset) | [**Supported Databases**](#supported-databases) | [**Installation and Configuration**](#installation-and-configuration) | [**Release Notes**](https://github.com/apache/superset/blob/master/RELEASING/README.md#release-notes-for-recent-releases) | [**Get Involved**](#get-involved) | [**Contributor Guide**](#contributor-guide) | [**Resources**](#resources) | [**Organizations Using Superset**](https://github.com/apache/superset/blob/master/RESOURCES/INTHEWILD.md)

Why Superset?[​](#why-superset "Direct link to Why Superset?")
--------------------------------------------------------------

Superset is a modern data exploration and data visualization platform. Superset can replace or augment proprietary business intelligence tools for many teams. Superset integrates well with a variety of data sources.

Superset provides:

*   A **no-code interface** for building charts quickly
*   A powerful, web-based **SQL Editor** for advanced querying
*   A **lightweight semantic layer** for quickly defining custom dimensions and metrics
*   Out of the box support for **nearly any SQL** database or data engine
*   A wide array of **beautiful visualizations** to showcase your data, ranging from simple bar charts to geospatial visualizations
*   Lightweight, configurable **caching layer** to help ease database load
*   Highly extensible **security roles and authentication** options
*   An **API** for programmatic customization
*   A **cloud-native architecture** designed from the ground up for scale

Screenshots & Gifs[​](#screenshots--gifs "Direct link to Screenshots & Gifs")
-----------------------------------------------------------------------------

**Video Overview**

https://superset.staged.apache.org/superset-video-4k.mp4**Large Gallery of Visualizations**

![Image 10](https://superset.apache.org/img/screenshots/gallery.jpg)

**Craft Beautiful, Dynamic Dashboards**

![Image 11](https://superset.apache.org/img/screenshots/slack_dash.jpg)

**No-Code Chart Builder**

![Image 12](https://superset.apache.org/img/screenshots/explore.jpg)

**Powerful SQL Editor**

![Image 13](https://superset.apache.org/img/screenshots/sql_lab.jpg)

Supported Databases[​](#supported-databases "Direct link to Supported Databases")
---------------------------------------------------------------------------------

Superset can query data from any SQL-speaking datastore or data engine (Presto, Trino, Athena, [and more](https://superset.apache.org/docs/configuration/databases)) that has a Python DB-API driver and a SQLAlchemy dialect.

Here are some of the major database solutions that are supported:

![Image 14: redshift](https://superset.apache.org/img/databases/redshift.png)![Image 15: google-biquery](https://superset.apache.org/img/databases/google-biquery.png)![Image 16: snowflake](https://superset.apache.org/img/databases/snowflake.png)![Image 17: trino](https://superset.apache.org/img/databases/trino.png)![Image 18: presto](https://superset.apache.org/img/databases/presto.png)![Image 19: databricks](https://superset.apache.org/img/databases/databricks.png)![Image 20: druid](https://superset.apache.org/img/databases/druid.png)![Image 21: firebolt](https://superset.apache.org/img/databases/firebolt.png)![Image 22: timescale](https://superset.apache.org/img/databases/timescale.png)![Image 23: rockset](https://superset.apache.org/img/databases/rockset.png)![Image 24: postgresql](https://superset.apache.org/img/databases/postgresql.png)![Image 25: mysql](https://superset.apache.org/img/databases/mysql.png)![Image 26: mssql-server](https://superset.apache.org/img/databases/mssql-server.png)![Image 27: db2](https://superset.apache.org/img/databases/imb-db2.svg)![Image 28: sqlite](https://superset.apache.org/img/databases/sqlite.png)![Image 29: sybase](https://superset.apache.org/img/databases/sybase.png)![Image 30: mariadb](https://superset.apache.org/img/databases/mariadb.png)![Image 31: vertica](https://superset.apache.org/img/databases/vertica.png)![Image 32: oracle](https://superset.apache.org/img/databases/oracle.png)![Image 33: firebird](https://superset.apache.org/img/databases/firebird.png)![Image 34: greenplum](https://superset.apache.org/img/databases/greenplum.png)![Image 35: clickhouse](https://superset.apache.org/img/databases/clickhouse.png)![Image 36: exasol](https://superset.apache.org/img/databases/exasol.png)![Image 37: monet-db](https://superset.apache.org/img/databases/monet-db.png)![Image 38: apache-kylin](https://superset.apache.org/img/databases/apache-kylin.png)![Image 39: hologres](https://superset.apache.org/img/databases/hologres.png)![Image 40: netezza](https://superset.apache.org/img/databases/netezza.png)![Image 41: pinot](https://superset.apache.org/img/databases/pinot.png)![Image 42: teradata](https://superset.apache.org/img/databases/teradata.png)![Image 43: yugabyte](https://superset.apache.org/img/databases/yugabyte.png)![Image 44: databend](https://superset.apache.org/img/databases/databend.png)![Image 45: starrocks](https://superset.apache.org/img/databases/starrocks.png)![Image 46: doris](https://superset.apache.org/img/databases/doris.png)

**A more comprehensive list of supported databases** along with the configuration instructions can be found [here](https://superset.apache.org/docs/configuration/databases).

Want to add support for your datastore or data engine? Read more [here](https://superset.apache.org/docs/frequently-asked-questions#does-superset-work-with-insert-database-engine-here) about the technical requirements.

Installation and Configuration[​](#installation-and-configuration "Direct link to Installation and Configuration")
------------------------------------------------------------------------------------------------------------------

[Extended documentation for Superset](https://superset.apache.org/docs/installation/docker-compose)

Get Involved[​](#get-involved "Direct link to Get Involved")
------------------------------------------------------------

*   Ask and answer questions on [StackOverflow](https://stackoverflow.com/questions/tagged/apache-superset) using the **apache-superset** tag
*   [Join our community's Slack](http://bit.ly/join-superset-slack) and please read our [Slack Community Guidelines](https://github.com/apache/superset/blob/master/CODE_OF_CONDUCT.md#slack-community-guidelines)
*   [Join our dev@superset.apache.org Mailing list](https://lists.apache.org/list.html?dev@superset.apache.org). To join, simply send an email to [dev-subscribe@superset.apache.org](mailto:dev-subscribe@superset.apache.org)
*   If you want to help troubleshoot GitHub Issues involving the numerous database drivers that Superset supports, please consider adding your name and the databases you have access to on the [Superset Database Familiarity Rolodex](https://docs.google.com/spreadsheets/d/1U1qxiLvOX0kBTUGME1AHHi6Ywel6ECF8xk_Qy-V9R8c/edit#gid=0)
*   Join Superset's Town Hall and [Operational Model](https://preset.io/blog/the-superset-operational-model-wants-you/) recurring meetings. Meeting info is available on the [Superset Community Calendar](https://superset.apache.org/community)

Contributor Guide[​](#contributor-guide "Direct link to Contributor Guide")
---------------------------------------------------------------------------

Interested in contributing? Check out our [CONTRIBUTING.md](https://github.com/apache/superset/blob/master/CONTRIBUTING.md) to find resources around contributing along with a detailed guide on how to set up a development environment.

Resources[​](#resources "Direct link to Resources")
---------------------------------------------------

*   [Superset "In the Wild"](https://github.com/apache/superset/blob/master/RESOURCES/INTHEWILD.md) - open a PR to add your org to the list!
*   [Feature Flags](https://github.com/apache/superset/blob/master/RESOURCES/FEATURE_FLAGS.md) - the status of Superset's Feature Flags.
*   [Standard Roles](https://github.com/apache/superset/blob/master/RESOURCES/STANDARD_ROLES.md) - How RBAC permissions map to roles.
*   [Superset Wiki](https://github.com/apache/superset/wiki) - Tons of additional community resources: best practices, community content and other information.
*   [Superset SIPs](https://github.com/orgs/apache/projects/170) - The status of Superset's SIPs (Superset Improvement Proposals) for both consensus and implementation status.

Understanding the Superset Points of View

*   [The Case for Dataset-Centric Visualization](https://preset.io/blog/dataset-centric-visualization/)
*   [Understanding the Superset Semantic Layer](https://preset.io/blog/understanding-superset-semantic-layer/)

*   Getting Started with Superset

    *   [Superset in 2 Minutes using Docker Compose](https://superset.apache.org/docs/installation/docker-compose#installing-superset-locally-using-docker-compose)
    *   [Installing Database Drivers](https://superset.apache.org/docs/configuration/databases#installing-database-drivers)
    *   [Building New Database Connectors](https://preset.io/blog/building-database-connector/)
    *   [Create Your First Dashboard](https://superset.apache.org/docs/using-superset/creating-your-first-dashboard/)
    *   [Comprehensive Tutorial for Contributing Code to Apache Superset](https://preset.io/blog/tutorial-contributing-code-to-apache-superset/)
*   [Resources to master Superset by Preset](https://preset.io/resources/)

*   Deploying Superset

    *   [Official Docker image](https://hub.docker.com/r/apache/superset)
    *   [Helm Chart](https://github.com/apache/superset/tree/master/helm/superset)
*   Recordings of Past [Superset Community Events](https://preset.io/events)

    *   [Mixed Time Series Charts](https://preset.io/events/mixed-time-series-visualization-in-superset-workshop/)
    *   [How the Bing Team Customized Superset for the Internal Self-Serve Data & Analytics Platform](https://preset.io/events/how-the-bing-team-heavily-customized-superset-for-their-internal-data/)
    *   [Live Demo: Visualizing MongoDB and Pinot Data using Trino](https://preset.io/events/2021-04-13-visualizing-mongodb-and-pinot-data-using-trino/)
    *   [Introduction to the Superset API](https://preset.io/events/introduction-to-the-superset-api/)
    *   [Building a Database Connector for Superset](https://preset.io/events/2021-02-16-building-a-database-connector-for-superset/)
*   Visualizations

    *   [Creating Viz Plugins](https://superset.apache.org/docs/contributing/creating-viz-plugins/)
    *   [Managing and Deploying Custom Viz Plugins](https://medium.com/nmc-techblog/apache-superset-manage-custom-viz-plugins-in-production-9fde1a708e55)
    *   [Why Apache Superset is Betting on Apache ECharts](https://preset.io/blog/2021-4-1-why-echarts/)
*   [Superset API](https://superset.apache.org/docs/rest-api)


Repo Activity[​](#repo-activity "Direct link to Repo Activity")
---------------------------------------------------------------

[![Image 47: Performance Stats of apache/superset - Last 28 days](https://next.ossinsight.io/widgets/official/compose-last-28-days-stats/thumbnail.png?repo_id=39464018&image_size=auto&color_scheme=light)](https://next.ossinsight.io/widgets/official/compose-last-28-days-stats?repo_id=39464018)![Image 48](https://static.scarf.sh/a.png?x-pxid=bc1c90cd-bc04-4e11-8c7b-289fb2839492)
