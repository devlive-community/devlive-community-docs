[TOC]

This chapter describes how to integrate SpotBugs into a Maven project.

Add spotbugs-maven-plugin to your pom.xml
---------------------------------------------------------------------------------------------------------------

Add `<plugin>` into your `pom.xml` like below:

```xml
<plugin>
  <groupId>com.github.spotbugs</groupId>
  <artifactId>spotbugs-maven-plugin</artifactId>
  <version>4.8.5.0</version>
  <dependencies>
    <!-- overwrite dependency on spotbugs if you want to specify the version of spotbugs -->
    <dependency>
      <groupId>com.github.spotbugs</groupId>
      <artifactId>spotbugs</artifactId>
      <version>4.8.5</version>
    </dependency>
  </dependencies>
</plugin>
```

Integrate Find Security Bugs into spotbugs-maven-plugin
-------------------------------------------------------------------------------------------------------------------------------------------

Are you looking for additional security detectors for SpotBugs? We suggest you to check the [Find Security Bugs](https://find-sec-bugs.github.io/) a SpotBugs plugin for security audits of Java web and Android applications. It can detect 138 different vulnerability types, including SQL/HQL Injection, Command Injection, XPath Injection, and Cryptography weaknesses.

To integrate Find Security Bugs into SpotBugs plugin, you can configure your `pom.xml` like below:

```xml
[...]
<build>
    <plugins>
        [...]
        <plugin>
            <groupId>com.github.spotbugs</groupId>
            <artifactId>spotbugs-maven-plugin</artifactId>
            <version>4.8.5.0</version>
            <configuration>
                <includeFilterFile>spotbugs-security-include.xml</includeFilterFile>
                <excludeFilterFile>spotbugs-security-exclude.xml</excludeFilterFile>
                <plugins>
                    <plugin>
                        <groupId>com.h3xstream.findsecbugs</groupId>
                        <artifactId>findsecbugs-plugin</artifactId>
                        <version>1.12.0</version>
                    </plugin>
                </plugins>
            </configuration>
        </plugin>
    </plugins>
</build>
```

The `<plugins>` option defines a collection of PluginArtifact to work on. Please, specify “Find Security Bugs” by adding its groupId, artifactId, version.

The `<includeFilterFile>` and `<excludeFilterFile>` specify the filter files to include and exclude bug reports, respectively (see [Filter file](https://spotbugs.readthedocs.io/en/latest/filter.html) for more details). Optionally, you can limit the research to the security category by adding files like below:

_spotbugs-security-include.xml_

```xml
<FindBugsFilter>
    <Match>
        <Bug category="SECURITY"/>
    </Match>
</FindBugsFilter>
```

_spotbugs-security-exclude.xml_

```xml
<FindBugsFilter>
</FindBugsFilter>
```

Goals of spotbugs-maven-plugin
-----------------------------------------------------------------------------------------

### spotbugs goal

`spotbugs` goal analyses target project by SpotBugs. For detail, please refer [spotbugs goal description in maven site](https://spotbugs.github.io/spotbugs-maven-plugin/spotbugs-mojo.html).

### check goal

`check` goal runs analysis like `spotbugs` goal, and make the build failed if it found any bugs. For detail, please refer [check goal description in maven site](https://spotbugs.github.io/spotbugs-maven-plugin/check-mojo.html).

### gui goal

`gui` goal launches SpotBugs GUI to check analysis result. For detail, please refer [gui goal description in maven site](https://spotbugs.github.io/spotbugs-maven-plugin/gui-mojo.html).

### help goal

`help` goal displays usage of this Maven plugin.
