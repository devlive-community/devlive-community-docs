[TOC]

Any application will require access to persisted objects. The JDO API provides several ways to do this

### Retrieve an object from its identity

The simplest form of object retrieval is where we have the identity. This is simply

    Person per = (Person)pm.getObjectById(identity);

or

    Person per = pm.getObjectById(Person.class, identity);

If the object is in the JDO cache (Level 1 or Level 2) then it is retrieved from there, otherwise the JDO implementation goes to the datastore. When the object is retrieved its fields are populated according to its [Fetch Plan]($Fetch-Plan-Groups).

### Retrieve an object based on its Extent

An **Extent** is a collection of objects of a particular type of object that have been persisted. When you define the MetaData for a class you can define if the class requires an Extent. The default is true. You access the Extent as follows

    Extent ex = pm.getExtent(MyClass.class, true);
    Iterator iter = ex.iterator();
    while (iter.hasNext())
    {
        MyClass obj = (MyClass)iter.next();
        ...
    }

The second argument in the _getExtent_ call is whether to include instances of subclasses. An Extent is useful where you want to restrict a Query to query over just that set of objects. It can also be used where you just want to retrieve all persisted objects of a type (as an alternative to using a Query).

### Retrieve an object based on a query criteria

Where we want to retrieve all objects based on some criteria (e.g all objects of class A where field 'x' of A is a certain value) we need to use a query language and the [JDO Query API]($Query-API). The JDO API provides the [JDOQL]($JDOQL) object-based query language where you express your query in terms of classes and fields you are using. Dependent on your JDO provider and the datastore being used you may also be able to use a (native) query language such as [SQL]($SQL), expressing your query in terms of datastore tables/columns.

To give an example of a JDOQL query

    Query q = pm.newQuery(MyClass.class, "field1 < value");
    q.declareParameters("int value");
    List results = q.execute(205);
    Iterator iter = results.iterator();
    while (iter.hasNext())
    {
        MyClass obj = (MyClass)iter.next();
    }

If the objects found by the query are in the JDO cache then they are retrieved from there, otherwise the JDO implementation goes to the datastore. When the objects are retrieved their fields are populated according to the Fetch Group.