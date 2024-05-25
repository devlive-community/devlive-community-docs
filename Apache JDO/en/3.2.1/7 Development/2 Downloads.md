[TOC]

To develop your own code to use or implement JDO, you can use the links below to download Apache JDO from an official ASF download site. If you are using Maven, you can declare a dependency using the instructions below.

If you intend to develop JDO (make modifications to the JDO code), you should clone the [public repository](https://db.apache.org/jdo/source-code.html) and submit pull requests if desired.

Please see instruction below for [verifying the integrity](#Verifying) of the distribution files after downloading any artifacts.

### Maven (convenience binary)

The most convenient way to use JDO is to configure your project using Maven. The JDO API can be downloaded automatically by maven and placed into your local maven repository if you include the proper dependency in your maven project definition. For example:

```auto
<dependency>
  <groupId>javax.jdo</groupId>
  <artifactId>jdo-api</artifactId>
  <version>3.2.1</version>
</dependency>
```

### About JDO Releases

A release of JDO includes the JDO API and the Technology Compatibility Kit (TCK). The TCK is available only in source form. The API project is available as source and as a jar file using the standard Maven dependency protocol.

+   The `jdo-api.jar` file is the only artifact needed for users who wish to compile their programs using the JDO API. It can be downloaded from maven, or it can be built manually from the source code.
+   The TCK project contains the JDO Technology Compatibility Kit.

Distributions have all code in a single download.

### Verifying Releases

It is essential that you verify the integrity of the downloaded files using the PGP signature.

The PGP signatures can be verified using PGP or GPG. First download the [KEYS](https://downloads.apache.org/db/jdo/KEYS) as well as the `asc` signature file for the particular distribution. Make sure you get these files from the [Apache downbload area](https://downloads.apache.org/db/jdo/), rather than from a mirror. Then verify the signatures using these commands (depending on your tool set):

```auto
% pgpk -a KEYS
% pgpv release_artifact.asc
```

```auto
% pgp -ka KEYS
% pgp release_artifact.asc
```

```auto
% gpg --import KEYS
% gpg --verify release_artifact.asc
```
