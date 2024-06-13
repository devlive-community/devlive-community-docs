[TOC]

This chapter explains how to install SpotBugs.

Extracting the Distribution[](#extracting-the-distribution "Link to this heading")
-----------------------------------------------------------------------------------

The easiest way to install SpotBugs is to download a binary distribution. Binary distributions are available in [gzipped tar format](https://github.com/spotbugs/spotbugs/releases/download/4.8.5/spotbugs-4.8.5.tgz) and [zip format](https://github.com/spotbugs/spotbugs/releases/download/4.8.5/spotbugs-4.8.5.zip). Once you have downloaded a binary distribution, extract it into a directory of your choice.

Extracting a gzipped tar format distribution:

```bash
$ gunzip -c spotbugs-4.8.5.tgz | tar xvf -
```

Extracting a zip format distribution:

```bash
C:\\Software\> unzip spotbugs\-4.8.5.zip
```

Usually, extracting a binary distribution will create a directory ending in spotbugs-4.8.5. For example, if you extracted the binary distribution from the C:\\Software directory, then the SpotBugs software will be extracted into the directory C:\\Software\\spotbugs-4.8.5. This directory is the SpotBugs home directory. We’ll refer to it as `$SPOTBUGS_HOME` (or `%SPOTBUGS_HOME%` for Windows) throughout this manual.