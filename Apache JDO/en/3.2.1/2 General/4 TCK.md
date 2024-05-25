[TOC]

In order to demonstrate compliance with the Java Data Objects specification, an implementation must pass all of the tests in the Technology Compatibility Kit (TCK). The TCK is released as a packaged Java source tree. Maven is the driver of a test run. You must download and install [Maven 2+](http://maven.apache.org/)before running the TCK.

### Running the TCK

To run the Technology Compatibility Kit:

1.  Check out the JDO source code from the most recent branch. See [Source Code](https://db.apache.org/jdo/source-code.html) for instructions on checking out code.

2.  Follow the instructions in the Prerequisites section of [README.md](https://github.com/apache/db-jdo/blob/main/README.md)

3.  Follow the procedure in [RunRules.md](https://github.com/apache/db-jdo/blob/main/tck/RunRules.md) in the tck directory.


### Demonstrating Compliance

Vendors must post test results on a publicly accessible web site for examination by the public. The posting includes the output of the test run, which consists of multiple log files containing configuration information and test results. For an example of the required posting, please see [](https://db.apache.org/jdo/tck/final)[http://db.apache.org/jdo/tck/final](http://db.apache.org/jdo/tck/final).
