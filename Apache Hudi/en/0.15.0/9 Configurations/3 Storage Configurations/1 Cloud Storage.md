[TOC]


## Talking to Cloud Storage

Immaterial of whether RDD/WriteClient APIs or Datasource is used, the following information helps configure access
to cloud stores.

* [AWS S3]($AWS-S3) <br/>
  Configurations required for S3 and Hudi co-operability.
* [Google Cloud Storage]($Google-Cloud) <br/>
  Configurations required for GCS and Hudi co-operability.
* [Alibaba Cloud OSS]($Alibaba-Cloud) <br/>
  Configurations required for OSS and Hudi co-operability.
* [Microsoft Azure]($Microsoft-Azure) <br/>
  Configurations required for Azure and Hudi co-operability.
* [Tencent Cloud Object Storage]($Tencent-Cloud) <br/>
  Configurations required for COS and Hudi co-operability.
* [IBM Cloud Object Storage]($IBM-Cloud) <br/>
  Configurations required for IBM Cloud Object Storage and Hudi co-operability.
* [Baidu Cloud Object Storage]($Baidu-Cloud) <br/>
  Configurations required for BOS and Hudi co-operability.
* [JuiceFS]($JuiceFS) <br/>
  Configurations required for JuiceFS and Hudi co-operability.
* [Oracle Cloud Infrastructure]($Oracle-Cloud-Infrastructure) <br/>
  Configurations required for OCI and Hudi co-operability.

> Many cloud object storage systems like [Amazon S3](https://docs.aws.amazon.com/s3/) allow you to set
> lifecycle policies, such as [S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html),
> to manage objects. One of the policies is related to object expiration. If your organisation has configured such policies,
> then please ensure to exclude (or have a longer expiry period) for Hudi tables.

