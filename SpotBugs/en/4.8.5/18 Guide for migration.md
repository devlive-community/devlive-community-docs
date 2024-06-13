[TOC]

Guide for migration from SpotBugs 3.1 to 4.0
============================================

for SpotBugs Users
------------------

* SpotBugs now use SLF4J instead of calling STDERR/STDOUT directly. So when you run SpotBugs, it is recommended to have a SLF4J binding in classpath.
* SQL files in SpotBugs project are dropped. Generally it does not affect your usage.
* JNLP (Applet) support is dropped.

for Plugin Developers
---------------------

* The `speed` attribute of `Detector` element in `findbugs.xml` is deprecated.
* The dependency on `jaxen` has been changed to `runtime` scope. Generally it does not affect your project because SpotBugs does not depend on it directly.
* The dependency on `Saxon-HE` has added as a `runtime` scope dependency.
* Some deprecated APIs have been removed, refer the javadoc and migrate to preferred API before you migrate to SpotBugs 4.0.

Guide for migration from FindBugs 3.0 to SpotBugs 3.1
=====================================================

com.google.code.findbugs:findbugs
---------------------------------

Simply replace ``com.google.code.findbugs:findbugs`` with ``com.github.spotbugs:spotbugs``.

```xml
<!-- for Maven -->
<dependency>
  <groupId>com.github.spotbugs</groupId>
  <artifactId>spotbugs</artifactId>
  <version>4.8.5</version>
</dependency>
```

```xml
// for Gradle
compile 'com.github.spotbugs:spotbugs:4.8.5'
```

com.google.code.findbugs:jsr305
-------------------------------

JSR305 is already Dormant status, so SpotBugs does not release ``jsr305`` jar file.
Please continue using findbugs' one.

com.google.code.findbugs:findbugs-annotations
---------------------------------------------

Please depend on ``spotbugs-annotations`` instead.

```xml
<!-- for Maven -->
<dependency>
  <groupId>com.github.spotbugs</groupId>
  <artifactId>spotbugs-annotations</artifactId>
  <version>4.8.5</version>
  <optional>true</optional>
</dependency>
```

```xml
// for Gradle
compileOnly 'com.github.spotbugs:spotbugs-annotations:4.8.5'
```

com.google.code.findbugs:annotations
------------------------------------

Please depend on both of ``spotbugs-annotations`` and ``com.github.stephenc.jcip:jcip-annotations:1.0-1`` instead.

```xml
<!-- for Maven -->
<dependency>
  <groupId>com.github.stephenc.jcip</groupId>
  <artifactId>jcip-annotations</artifactId>
  <version>1.0-1</version>
  <optional>true</optional>
</dependency>
<dependency>
  <groupId>com.github.spotbugs</groupId>
  <artifactId>spotbugs-annotations</artifactId>
  <version>4.8.5</version>
  <optional>true</optional>
</dependency>
```

```xml
// for Gradle
compileOnly 'com.github.stephenc.jcip:jcip-annotations:1.0-1'
compileOnly 'com.github.spotbugs:spotbugs-annotations:4.8.5'
```

FindBugs Ant task
-----------------

Please replace ``findbugs-ant.jar`` with ``spotbugs-ant.jar``.

```xml
<taskdef
  resource="edu/umd/cs/findbugs/anttask/tasks.properties"
  classpath="path/to/spotbugs-ant.jar" />
<property name="spotbugs.home" value="/path/to/spotbugs/home" />

<target name="spotbugs" depends="jar">
  <spotbugs home="${spotbugs.home}"
            output="xml"
            outputFile="bcel-fb.xml" >
    <auxClasspath path="${basedir}/lib/Regex.jar" />
    <sourcePath path="${basedir}/src/java" />
    <class location="${basedir}/bin/bcel.jar" />
  </spotbugs>
</target>
```

FindBugs Maven plugin
---------------------

Please use `com.github.spotbugs:spotbugs-maven-plugin` instead of `org.codehaus.mojo:findbugs-maven-plugin`.

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

FindBugs Gradle plugin
----------------------

Please use spotbugs plugin found on https://plugins.gradle.org/plugin/com.github.spotbugs

```xml
plugins {
  id  'com.github.spotbugs' version '6.0.14'
}
spotbugs {
  toolVersion = '4.8.5'
}

// To generate an HTML report and XML report
tasks.withType(com.github.spotbugs.snom.SpotBugsTask) {
  reports {
    xml.required.set(true)
    html.required.set(true)
  }
}
```

FindBugs Eclipse plugin
-----------------------

Please use following update site instead.

* https://spotbugs.github.io/eclipse/ (to use stable version)
* https://spotbugs.github.io/eclipse-candidate/ (to use candidate version)
* https://spotbugs.github.io/eclipse-latest/ (to use latest build)
