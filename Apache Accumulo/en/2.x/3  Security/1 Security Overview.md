[TOC]

Security Overview
=================

Accumulo has the following security features:

*   Only [authenticated]($Authentication) users can access Accumulo.
    *   [Kerberos]($Kerberos) can be enabled to replace Accumulo’s default, password-based authentication
*   Users can only perform actions if they are given [permission]($Permissions).
*   Users can only view [labeled data]($Authentication#security-labels) that they are [authorized]($Authentication) to see.
*   Data can be encrypted [on disk]($On-Disk-Encryption) and [over-the-wire]($Wire-Encryption)

Implementation
---------------------------------------------------------------------------------------

Below is a description of how security is implemented in Accumulo.

Once a user is authenticated by the [Authenticator](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/Authenticator.html), the user has access to the other actions within Accumulo. All actions in Accumulo are ACLed, and this ACL check is handled by the [PermissionHandler](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/PermissionHandler.html). This is what manages all of the [permissions]($Permissions), which are divided in system and per table level. From there, if a user is doing an action which requires authorizations, the [Authorizor](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/Authorizor.html) is queried to determine what authorizations the user has.

This setup allows a variety of different mechanisms to be used for handling different aspects of Accumulo’s security. A system like [Kerberos](https://accumulo.apache.org/docs/2.x/security/kerberos) can be used for [authentication](https://accumulo.apache.org/docs/2.x/security/authentication), then a system like LDAP could be used to determine if a user has a specific permission, and then it may default back to the default [Authorizor](https://static.javadoc.io/org.apache.accumulo/accumulo-server-base/2.1.2/org/apache/accumulo/server/security/handler/Authorizor.html) to determine what Authorizations a user is ultimately allowed to use. This is a pluggable system so custom components can be created depending on your need.
