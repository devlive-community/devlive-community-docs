[TOC]

To build and run your JDO application, you need a JDO implementation. This page lists commercial and non-commercial JDO implementations. For information on how vendors certify compliance with the JDO specifications, see [TCK](https://db.apache.org/jdo/tck.html).

### JDO Reference Implementations

- JDO 1.0 : [FOStore](http://jcp.org/aboutJava/communityprocess/final/jsr012/index2.html) 
- JDO 2.0 : [JPOX 1.1](https://sourceforge.net/projects/jpox/) 
- JDO 2.1 : [JPOX 1.2](https://sourceforge.net/projects/jpox/)
- JDO 2.2 : [DataNucleus AccessPlatform 1.0](https://www.datanucleus.org/documentation/products.html)
- JDO 3.0 : [DataNucleus AccessPlatform 2.1](https://www.datanucleus.org/documentation/products.html)
- JDO 3.1 : [DataNucleus AccessPlatform 3.2](https://www.datanucleus.org/documentation/products.html)
- JDO 3.2 : [DataNucleus AccessPlatform 5.2](https://www.datanucleus.org/products/accessplatform_5_2/index.html)

### Implementations

Below is a list of known implementations of JDO, showing the level of JDO that the implementation tries to implement, and the type of datastore that the implementation supports. You should check the vendors website for details of whether the implementation is fully compliant with the specification claimed - Apache JDO simply provides visibility of known implementations.

<table class="tableblock frame-all grid-all stretch">
  <colgroup>
    <col style="width: 25%;">
      <col style="width: 25%;">
        <col style="width: 25%;">
          <col style="width: 25%;"></colgroup>
  <thead>
    <tr>
      <th class="tableblock halign-left valign-top">Name</th>
      <th class="tableblock halign-left valign-top">License</th>
      <th class="tableblock halign-left valign-top">JDO Spec</th>
      <th class="tableblock halign-left valign-top">Datastore(s)</th></tr>
  </thead>
  <tbody>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.datanucleus.org">DataNucleus Access Platform</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">NonCommercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0, 2.0, 2.1, 2.2, 3.0, 3.1, 3.2</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS, db4o, NeoDatis, LDAP, Excel XLS, Excel OOXML, ODF, XML, JSON, Google BigTable, HBase, Amazon S3, MongoDB, GoogleStorage, Cassandra, OrientDB, Salesforce.com, Neo4j</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.jdoinstruments.org/">JDOInstruments</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">NonCommercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">JDOInstruments</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.jpox.org">
            <em>JPOX</em></a>
        </p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">NonCommercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0, 2.0, 2.1</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS, db4o</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.bea.com/kodo">
            <em>Kodo</em></a>
        </p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0, 2.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS, XML</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.objectdb.com/">ObjectDB for Java/JDO</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0, 2.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">ObjectDB</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.objectivity.com/pages/object-database-solutions/java-data-objects.asp">Objectivity</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">ObjectivityDB</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.orientechnologies.com/cms/">Orient</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Orient</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://pejava.tripod.com/index.html">
            <em>hywy’s PE:J</em></a>
        </p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.signsoft.de/signsoft/en/intelliBO/">
            <em>SignSoft intelliBO</em></a>
        </p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">intelliBO</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://speedo.objectweb.org/">
            <em>Speedo</em></a>
        </p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">NonCommercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://tjdo.sourceforge.net/">
            <em>TJDO</em></a>
        </p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">NonCommercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.versant.com/en_US/products/objectdatabase/">Versant</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0, 2.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Versant Object Database</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.xcalia.com/xdn/specs/jdo">Xcalia</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">Commercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">1.0, 2.0</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">RDBMS, XML, Versant ODBMS, Jalisto, Web services, mainframe transactions and screens (CICS, IMS…​), packaged applications (ERP, CRM,SFA…​), components (EJB…​).</p></td>
    </tr>
    <tr>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">
          <a href="http://www.zoodb.org">ZooDB</a></p>
      </td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">NonCommercial</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">3.0 (partial), 3.1 (Partial)</p></td>
      <td class="tableblock halign-left valign-top">
        <p class="tableblock">ZooDB ODBMS</p></td>
    </tr>
  </tbody>
</table>
