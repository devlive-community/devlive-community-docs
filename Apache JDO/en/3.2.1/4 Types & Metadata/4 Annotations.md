[TOC]

One of the things that JDK 1.5 provides that can be of some use is annotations, and JDO provides its own set. When selecting to use annotations please bear in mind the following :

+   You must have the **jdo-api** jar in your CLASSPATH since this provides the annotations
+   Annotations should really only be used for attributes of persistence that you won’t be changing at deployment. Things such as table and column names shouldn’t really be specified using annotations although it is permitted. Instead it would be better to put such information in an ORM MetaData file.
+   Annotations can be added in two places – for the class as a whole, or for a field in particular.
+   You can annotate fields or getters with field-level information. If you annotate fields then the fields are processed for persistence. If you annotate the methods (getters) then the methods (properties) are processed for persistence.
+   Annotations are prefixed by the @ symbol and can take properties (in brackets after the name, comma-separated)

| Annotation | Class/Field/Method | Description |
| --- | --- | --- |
|[@PersistenceCapable](#PersistenceCapable)|Class|Specifies that the class/interface is persistent. In the case of an interface this would utilise JDO2’s "persistent-interface" capabilities|
|[@PersistenceAware](#PersistenceAware)|Class|Specifies that the class is not persistent but needs to be able to access fields of persistent classes|
|[@Cacheable](#Cacheable_Class)|Class|Specifies whether this class can be cached in a Level 2 cache or not.|
|[@EmbeddedOnly](#EmbeddedOnly)| Class | Specifies that the class is persistent and can only be persisted embedded in another persistent class |
|[@DatastoreIdentity](#DatastoreIdentity)| Class | Specifies the details for generating datastore-identity for this class |
|[@Version](#Version)|Class|Specifies any versioning process for objects of this class|
|[@FetchPlans](#FetchPlans)|Class|Defines a series of fetch plans|
|[@FetchPlan](#FetchPlan)|Class|Defines a fetch plan|
|[@FetchGroups](#FetchGroups)|Class|Defines a series of fetch groups for this class|
|[@FetchGroup](#FetchGroup)|Class|Defines a fetch group for this class|
|[@Sequence](#Sequence)| Class | Defines a sequence for use by this class |
|[@Queries](#Queries)| Class | Defines a series of named queries for this class |
|[@Query](#Query)| Class | Defines a named query for this class |
|[@Inheritance](#Inheritance)| Class | Specifies the inheritance model for persisting this class |
|[@Discriminator](#Discriminator)| Class | Specifies any discriminator for this class to be used for determining object types |
|[@PrimaryKey](#PrimaryKey_Class)| Class | ORM : Defines the primary key constraint for this class |
|[@Indices](#Indices)| Class | ORM : Defines a series of indices for this class |
|[@Index](#Index_Class)| Class | ORM : Defines an index for the class as a whole (typically a composite index)|
|[@Uniques](#Uniques)| Class | ORM : Defines a series of unique constraints for this class |
|[@Unique](#Unique_Class)| Class | ORM : Defines a unique constraint for the class as a whole (typically a composite)|
|[@ForeignKeys](#ForeignKeys)|Class|ORM : Defines a series of foreign-keys (typically for non-mapped columns/tables)|
|[@ForeignKey](#ForeignKey_Class)|Class|ORM : Defines a foreign-key for the class as a whole (typically for non-mapped columns/tables)|
|[@Joins](#Joins)|Class|ORM : Defines a series of joins to secondary tables from this table|
|[@Join](#Join_Class)|Class|ORM : Defines a join to a secondary table from this table|
|[@Columns](#Columns)| Class | ORM : Defines a series of columns that don’t have associated fields ("unmapped columns")|
|[@Persistent](#Persistent)| Field/Method | Defines the persistence for a field/property of the class |
|[@Serialized](#Serialized)| Field/Method | Defines this field as being stored serialised |
|[@NotPersistent](#NotPersistent)| Field/Method | Defines this field as being not persisted |
|[@Transactional](#Transactional)| Field/Method | Defines this field as being transactional (not persisted, but managed)|
|[@Cacheable](#Cacheable)| Field/Method | Specifies whether this field/property can be cached in a Level 2 cache or not. |
|[@PrimaryKey](#PrimaryKey)| Field/Method | Defines this field as being (part of) the primary key |
|[@Element](#Element)| Field/Method | Defines the details of elements of an array/collection stored in this field |
|[@Key](#Key)| Field/Method | Defines the details of keys of a map stored in this field |
|[@Value](#Value)| Field/Method | Defines the details of values of a map stored in this field |
|[@Order](#Order)| Field/Method | ORM : Defines the details of ordering of an array/collection stored in this field |
|[@Join](#Join)| Field/Method | ORM : Defines the join to a join table for a collection/array/map |
|[@Embedded](#Embedded)| Field/Method | ORM : Defines that this field is embedded and how it is embedded |
|[@Columns](#Columns)| Field/Method | ORM : Defines a series of columns where a field is persisted |
|[@Column](#Column)| Field/Method | ORM : Defines a column where a field is persisted |
|[@Index](#Index)| Field/Method | ORM : Defines an index for the field |
|[@Unique](#Unique)| Field/Method | ORM : Defines a unique constraint for the field |
|[@ForeignKey](#ForeignKey)| Field/Method | ORM : Defines a foreign key for the field |
|[@Extensions](#Extensions)| Class/Field/Method | Defines a series of JDO extensions |
|[@Extension](#Extension)| Class/Field/Method | Defines a JDO extension |

### @PersistenceCapable

This annotation is used when you want to mark a class as persistent. It equates to the `<class>` MetaData element (though with only some of its attributes). Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | -- |
|requiresExtent|String|Whether an extent is required for this class|true|
|embeddedOnly|String|Whether objects of this class can only be stored embedded in other objects|false|
|detachable|String|Whether objects of this class can be detached|false|
|identityType|IdentityType|Type of identity (APPLICATION, DATASTORE, NONDURABLE)|DATASTORE|
|objectIdClass|Class|Object-id class|  |
|table|String|ORM : Name of the table where this class is persisted|  |
|catalog|String|ORM : Name of the catalog where this table is persisted|  |
|schema|String|ORM : Name of the schema where this table is persisted|  |
|cacheable|String|Whether the class can be L2 cached. **From JDO2.2**|**true**|
|false|serializeRead|String|Whether to default reads of this object type to lock the object|
|false|extensions|[Extension](#Extension)\[\]|Vendor extensions|

```java
@PersistenceCapable(identityType=IdentityType.APPLICATION)
public class MyClass
{
...
}
```

### @PersistenceAware

This annotation is used when you want to mark a class as being used in persistence but not being persistable. That is "persistence-aware" in JDO terminology. It has no attributes. Specified on the **class**.

```java
@PersistenceAware
public class MyClass
{
...
}
```

See the documentation for [Class Types]($Types-Of-Classes)

### @Cacheable

This annotation is a shortcut for @PersistenceCapable(cacheable={value}) specifying whether the class can be cached in a Level 2 cache. Specified on the **class**. The default

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|String|Whether the class is cacheable|**true**|

```java
@Cacheable("false")
public class MyClass
{
...
}
```

### @EmbeddedOnly

This annotation is a shortcut for @PersistenceCapable(embeddedOnly="true") meaning that the class can only be persisted embedded into another class. It has no attributes. Specified on the **class**.

```java
@EmbeddedOnly
public class MyClass
{
...
}
```

### @Inheritance

Annotation used to define the inheritance for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|strategy|InheritanceStrategy|The inheritance strategy (NEW\_TABLE, SUBCLASS\_TABLE, SUPERCLASS\_TABLE)|  |
|customStrategy|String|Name of a custom inheritance strategy (depending on what your JDO implementation supports|  |

```java
@PersistenceCapable
@Inheritance(strategy=InheritanceStrategy.NEW_TABLE)
public class MyClass
{
...
}
```

### @Discriminator

Annotation used to define a discriminator to be stored with instances of this class and is used to determine the types of the objects being stored. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|strategy|DiscriminatorStrategy|The discriminator strategy (VALUE\_MAP, CLASS\_NAME, NONE)|  |
|value|String|Value to use for instances of this type when using strategy of VALUE\_MAP|  |
|column|String|ORM : Name of the column to use to store the discriminator|  |
|indexed|String|ORM : Whether the discriminator column is to be indexed|  |
|columns|[Column](#Column)\[\]|ORM : Column definitions used for storing the discriminator|  |

```java
@PersistenceCapable
@Inheritance(strategy=InheritanceStrategy.NEW_TABLE)
@Discriminator(strategy=DiscriminatorStrategy.CLASS_NAME)
public class MyClass
{
...
}
```

### @DatastoreIdentity

Annotation used to define the identity when using datastore-identity for the class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|strategy|IdGeneratorStrategy|The inheritance strategy (NATIVE, SEQUENCE, IDENTITY, INCREMENT, UUIDSTRING, UUIDHEX)|  |
|customStrategy|String|Name of a custom id generation strategy (e.g "max", "auid"). This overrides the value of "strategy"|  |
|sequence|String|Name of the sequence to use (when using SEQUENCE strategy) - refer to @Sequence|  |
|column|String|ORM : Name of the column for the datastore identity|  |
|columns|[Column](#Column)\[\]|ORM : Column definition for the column(s) for the datastore identity|  |
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

```java
@PersistenceCapable
@DatastoreIdentity(strategy=IdGeneratorStrategy.INCREMENT)
public class MyClass
{
...
}
```

### @Version

Annotation used to define the versioning details for use with optimistic transactions. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|strategy|VersionStrategy|The version strategy (NONE, STATE\_IMAGE, DATE\_TIME, VERSION\_NUMBER)|  |
|indexed|String|Whether the version column(s) is indexed|  |
|column | String | ORM : Name of the column for the version |  |
|columns |[Column](#Column)\[\] | ORM : Column definition for the column(s) for the version |  |
|extensions |[Extension](#Extension)\[\] | Vendor extensions |  |

```java
@PersistenceCapable
@Version(strategy=VersionStrategy.VERSION_NUMBER)
public class MyClass
{
...
}
```

See the documentation for [transactions]($Transactions)

### @PrimaryKey

Annotation used to define the primary key constraint for a class. Maps across to the `<primary-key>` MetaData element. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | --- | --- | --- |
|name|String|ORM : Name of the primary key constraint|  |
|column|String|ORM : Name of the column for this key|  |
|columns|[Column](#Column)\[\]|ORM : Column definition for the column(s) of this key|  |

```java
@PersistenceCapable
@PrimaryKey(name="MYCLASS_PK")
public class MyClass
{
...
}
```

### @FetchPlans

Annotation used to define a set of fetch plans. Specified on the **class**. Used by named queries

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[FetchPlan](#FetchPlan)\[\]|Array of fetch plans - see @FetchPlan annotation|  |

```java
@PersistenceCapable
@FetchPlans({@FetchPlan(name="plan_3", maxFetchDepth=3, fetchGroups={"group1", "group4"}),
@FetchPlan(name="plan_4", maxFetchDepth=2, fetchGroups={"group1", "group2"})})
public class MyClass
{
...
}
```

See the documentation for [FetchGroups]($Fetch-Plan-Groups)

### @FetchPlan

Annotation used to define a fetch plan Is equivalent to the `<fetch-plan>` metadata element. Specified on the **class**. Used by named queries

| Attribute | Type | Description | Default |
| -- | -- | --- | -- |
|name|String|Name of the FetchPlan| |
|maxFetchDepth|int|Maximum fetch depth|1|
| fetchSize | int | Size hint for fetching query result sets | 0 |
| fetchGroups | String\[\] | Names of the fetch groups included in this FetchPlan. | |

```java
@PersistenceCapable
@FetchPlan(name="plan_3", maxFetchDepth=3, fetchGroups={"group1", "group4"})
public class MyClass
{
...
}
```

See the documentation for [FetchGroups]($Fetch-Plan-Groups)

### @FetchGroups

Annotation used to define a set of fetch groups for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[FetchGroup](#FetchGroup)\[\]|Array of fetch groups - see @FetchGroup annotation|  |

```java
@PersistenceCapable
@FetchGroups({@FetchGroup(name="one_two", members={@Persistent(name="field1"), @Persistent(name="field2")}),
@FetchGroup(name="three", members={@Persistent(name="field3")})})
public class MyClass
{
@Persistent
String field1;

    @Persistent
    String field2;

    @Persistent
    String field3;
    ...
}
```

See the documentation for [FetchGroups]($Fetch-Plan-Groups)

### @FetchGroup

Annotation used to define a fetch group. Is equivalent to the `<fetch-group>` metadata element. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | --- | --- | --- |
|name|String|Name of the fetch group|  |
|postLoad|String|Whether to call jdoPostLoad after loading this fetch group|  |
|members|[Persistent](#Persistent)\[\]|Definitions of the fields/properties to include in this fetch group|  |

```java
@PersistenceCapable
@FetchGroup(name="one_two", members={@Persistent(name="field1"), @Persistent(name="field2")})
public class MyClass
{
@Persistent
String field1;

    @Persistent
    String field2;
    ...
}
```

See the documentation for [FetchGroups]($Fetch-Plan-Groups)

### @Sequence

Annotation used to define a sequence generator. Is equivalent to the `<sequence>` metadata element. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | - | --- | - |
|name|String|Name of the sequence| |
|strategy|SequenceStrategy|Strategy for the sequence (NONTRANSACTIONAL, CONTIGUOUS, NONCONTIGUOUS)| |
|datastoreSequence|String|Name of a datastore sequence that this maps to| |
|factoryClass|Class|Factory class to use to generate the sequence| |
|initialValue|int|Initial value of the sequence|1|
|allocationSize|int|Allocation size of the sequence|50|
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

### @Queries

Annotation used to define a set of named queries for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[Query](#Query)\[\]|Array of queries - see @Query annotation|  |

```java
@PersistenceCapable
@Queries({@Query(name="PeopleCalledSmith", language="JDOQL",
value="SELECT FROM mydomain.Person WHERE surname == \"Smith\""),
@Query(name="PeopleCalledJones", language="JDOQL",
value="SELECT FROM mydomain.Person WHERE surname == \"Jones\"")})
public class Person
{
@Persistent
String surname;

    ...
}
```

### @Query

Annotation used to define a named query. Is equivalent to the `<query>` metadata element. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | --- | --- | --- |
|name|String|Name of the query|  |
|value|String|The query string itself|  |
|language|String|Language of the query (JDOQL, SQL, …)|JDOQL|
|unmodifiable|String|Whether the query is not modifiable at runtime|  |
|unique|String|Whether the query returns unique results (for SQL queries only)|  |
|resultClass|Class|Result class to use (for SQL queries only)|  |
|fetchPlan|String|Name of a named FetchPlan to use with this query|  |
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

```java
@PersistenceCapable
@Query(name="PeopleCalledSmith", language="JDOQL",
value="SELECT FROM mydomain.Person WHERE surname == \"Smith\"")
public class Person
{
@Persistent
String surname;

    ...
}
```

### @Indices

Annotation used to define a set of indices for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[Index](#Index_Class)\[\]|Array of indices - see @Index annotation|  |

```java
@PersistenceCapable
@Indices({@Index(name="MYINDEX_1", members={"field1","field2"}), @Index(name="MYINDEX\_2", members={"field3"})})
public class Person
{
...
}
```

### @Index

Annotation used to define an index for the class as a whole typically being a composite index across multiple columns or fields/properties. Is equivalent to the `<index>` metadata element when specified under class. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | --- | --- | --- |
|name|String|ORM : Name of the index|  |
|table|String|ORM : Name of the table for the index|  |
|unique|String|ORM : Whether the index is unique|  |
|members|String\[\]|ORM : Names of the fields/properties that make up this index|  |
|columns|[Column](#Column)\[\]|ORM : Columns that make up this index|  |

```java
@PersistenceCapable
@Index(name="MY_COMPOSITE_IDX", members={"field1", "field2"})
public class MyClass
{
@Persistent
String field1;

    @Persistent
    String field2;

    ...
}
```

### @Uniques

Annotation used to define a set of unique constraints for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[Unique](#Unique_Class)\[\]|Array of constraints - see @Unique annotation|  |

```java
@PersistenceCapable
@Uniques({@Unique(name="MYCONST_1", members={"field1","field2"}), @Unique(name="MYCONST_2", members={"field3"})})
public class Person
{
...
}
```

### @Unique

Annotation used to define a unique constraints for the class as a whole typically being a composite constraint across multiple columns or fields/properties. Is equivalent to the `<unique>` metadata element when specified under class. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | --- | --- | --- |
|name|String|ORM : Name of the constraint|  |
|table|String|ORM : Name of the table for the constraint|  |
|deferred|String|ORM : Whether the constraint is deferred|  |
|members|String\[\]|ORM : Names of the fields/properties that make up this constraint|  |
|columns|[Column](#Column)\[\]|ORM : Columns that make up this constraint|  |

```java
@PersistenceCapable
@Unique(name="MY_COMPOSITE_IDX", members={"field1", "field2"})
public class MyClass
{
@Persistent
String field1;

    @Persistent
    String field2;

    ...
}
```

### @ForeignKeys

Annotation used to define a set of foreign-key constraints for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[ForeignKey](#ForeignKey_Class)\[\]|Array of FK constraints - see @ForeignKey annotation|  |

### @ForeignKey

Annotation used to define a foreign-key constraint for the class. Specified on the **class**.

| Attribute | Type | Description | Default |
| -- | --- | --- | --- |
|name|String|ORM : Name of the constraint|  |
|table|String|ORM : Name of the table that the FK is to|  |
|deferred|String|ORM : Whether the constraint is deferred|  |
|unique|String|ORM : Whether the constraint is unique|  |
|deleteAction|ForeignKeyAction|ORM : Action to apply to the FK to be used on deleting|ForeignKeyAction.RESTRICT|
|updateAction|ForeignKeyAction|ORM : Action to apply to the FK to be used on updating|ForeignKeyAction.RESTRICT|
|members|String\[\]|ORM : Names of the fields/properties that compose this FK.|  |
|columns|[Column](#Column)\[\]|ORM : Columns that compose this FK.|  |

### @Joins

Annotation used to define a set of joins (to secondary tables) for a class. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[Join](#Join_Class)\[\]|Array of joins - see @Join annotation|  |

```java
@PersistenceCapable
@Joins({@Join(table="MY_OTHER_TABLE", column="MY_PK_COL"),
@Join(table="MY_SECOND_TABLE", column="MY_PK_COL")})
public class MyClass
{
@Persistent(table="MY_OTHER_TABLE")
String myField;

    @Persistent(table="MY_SECOND_TABLE")
    String myField2;
    ...
}
```

### @Join

Annotation used to specify a join for a secondary table. Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|table|String|ORM : Table name used when joining the PK of a FCO class table to a secondary table.|  |
|column|String|ORM : Name of the column used to join to the PK of the primary table (when only one column used)|  |
|outer|String|ORM : Whether to use an outer join when retrieving fields/properties stored in the secondary table|  |
|columns|[Column](#Column)\[\]|ORM : Name of the colums used to join to the PK of the primary table (when multiple columns used)|  |
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

```java
@PersistenceCapable(name="MYTABLE")
@Join(table="MY_OTHER_TABLE", column="MY_PK_COL")
public class MyClass
{
@Persistent(name="MY_OTHER_TABLE")
String myField;
...
}
```

### @Columns

Annotation used to define the columns which have no associated field in the class. User should specify a minimum of @Column "name", "jdbcType", and "insertValue". Specified on the **class**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|[Column](#Column)\[\]|Array of columns - see @Column annotation|  |

```java
@PersistenceCapable
@Columns(@Column(name="MY_OTHER_COL", jdbcType="VARCHAR", insertValue="N/A")
public class MyClass
{
...
}
```

### @Persistent

Annotation used to define the fields/properties to be persisted. Is equivalent to the `<field>` and `<property>` metadata elements. Specified on the **field/method**.

| Attribute      | Type        | Description | Default |
|----------------|-------------| -- | -- |
| persistenceModifier| PersistenceModifier|Whether the field is persistent (PERSISTENT, TRANSACTIONAL, NONE)|\[depends on field type\]|
| defaultFetchGroup | String      |Whether the field is part of the DFG|  |
| nullValue      | NullValue   |Required behaviour when inserting a null value for this field (NONE, EXCEPTION, DEFAULT).|NONE|
| embedded       | String      |Whether this field as a whole is embedded. Use @Embedded to specify details.|  |
| embeddedElement | String      |Whether the element stored in this collection/array field/property is embedded|  |
| embeddedKey    | String      |Whether the key stored in this map field/property is embedded|  |
| embeddedValue  | String      |Whether the value stored in this map field/property is embedded|  |
| serialized     | String      |Whether this field/property as a whole is serialised|  |
| serializedElement | String      |Whether the element stored in this collection/array field/property is serialised|  |
| serializedKey  | String      |Whether the key stored in this map field/property is serialised|  |
| serializedValue | String      |Whether the value stored in this map field/property is serialised|  |
| dependent      | String      |Whether this field is dependent, deleting the related object when deleting this object|  |
| dependentElement | String      |Whether the element stored in this field/property is dependent|  |
| dependentKey   | String      |Whether the key stored in this field/property is dependent|  |
| dependentValue | String      |Whether the value stored in this field/property is dependent|  |
| primaryKey     | String      |Whether this field is (part of) the primary key|false|
| valueStrategy  | IdGeneratorStrategy|Strategy to use when generating values for the field (NATIVE, SEQUENCE, IDENTITY, INCREMENT, UUIDSTRING, UUIDHEX)|  |
| customValueStrategy| String      |Name of a custom id generation strategy (e.g "max", "auid"). This overrides the value of "valueStrategy"|  |
| sequence       | String      |Name of the sequence when using valueStrategy of SEQUENCE - refer to @Sequence|  |
| types          |Class\[\]|Type(s) of field (when using interfaces/reference types).|  |
| mappedBy       |String|Field in other class when the relation is bidirectional to signify the owner of the relation|  |
| table          |String|ORM : Name of the table where this field is persisted. If this field is a collection/map/array then the table refers to a join table, otherwise this refers to a secondary table.|  |
| name           |String|Name of the field when defining an embedded field.|  |
| columns        |[Column](#Column)\[\]|ORM : Column definition(s) for the columns into which this field is persisted. This is only typically used when specifying columns of a field of an embedded class.|  |
|cacheable|String|Whether the field/property can be L2 cached. **From JDO2.2**|**true**|
|false|extensions|[Extension](#Extension)\[\]|Vendor extensions|
| |recursionDepth|int|Recursion depth for this field when fetching. **Only applicable when specified within @FetchGroup**|
|1|loadFetchGroup|String|Name of a fetch group to activate when a load of this field is initiated (due to it being currently unloaded). Not used for getObjectById, queries, extents etc. Better to use @FetchGroup and define your groups|

```java
@PersistenceCapable
public class MyClass
{
    @Persistent(primaryKey="true")
    String myField;
    ...
}
```

See the documentation for [Field Types]($Types-Of-Fields)

### @Serialized

This annotation is a shortcut for @Persistent(serialized="true") meaning that the field is stored serialized. It has no attributes. Specified on the **field/method**.

```java
@PersistenceCapable
public class MyClass
{
@Serialized
Object myField;
...
}
```

### @NotPersistent

This annotation is a shortcut for @Persistent(persistenceModifier=PersistenceModifier.NONE) meaning that the field/property is not persisted. It has no attributes. Specified on the **field/method**.

```java
@PersistenceCapable
public class MyClass
{
    @NotPersistent
    String myOtherField;
    ...
}
```

See the documentation for [Field Types]($Types-Of-Fields)

### @Transactional

This annotation is a shortcut for @Persistent(persistenceModifier=PersistenceModifier.TRANSACTIONAL) meaning that the field/property is not persisted yet managed. It has no attributes. Specified on the **field/method**.

```java
@PersistenceCapable
public class MyClass
{
    @Transactional
    String myOtherField;
    ...
}
```

See the documentation for [Field Types]($Types-Of-Fields)

### @Cacheable

This annotation is a shortcut for @Persistent(cacheable={value}) specifying whether the field/property can be cached in a Level 2 cache. Specified on the **field/property**. The default

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value|String|Whether the field/property is cacheable|**true**|

```java
public class MyClass
{
    @Cacheable("false")
    Collection elements;
    ...
}
```

### @PrimaryKey

This annotation is a shortcut for @Persistent(primaryKey="true") meaning that the field/property is part of the primary key for the class. No attributes are needed when specified like this. Specified on the **field/method**.

```java
@PersistenceCapable
public class MyClass
{
    @PrimaryKey
    String myOtherField;
    ...
}
```

### @Element

Annotation used to define the element for any collection/array to be persisted. Maps across to the `<collection>`, `<array>` and `<element>` MetaData elements. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|types|Class\[\]|Type(s) of element|When using an array is not needed. When using a collection will be taken from the collection definition if using generics, otherwise must be specified.|
|embedded|String|Whether the element is embedded into a join table|  |
|serialized|String|Whether the element is serialised into the join table|  |
|dependent|String|Whether the element objects are dependent when deleting the owner collection/array|  |
|mappedBy|String|Field in the element class that represents this object (when the relation is bidirectional)|  |
|embeddedMapping|[Embedded](#Embedded)\[\]|Definition of any embedding of the (persistable) element. Only 1 "Embedded" should be provided|  |
|table|String|ORM : Name of the table for this element|  |
|column|String|ORM : Name of the column for this element|  |
|foreignKey|String|ORM : Name of any foreign-key constraint to add|  |
|generateForeignKey|String|ORM : Whether to generate a FK constraint for the element (when not specifying the name)|  |
|deleteAction|ForeignKeyAction|ORM : Action to be applied to the foreign key for this element for action upon deletion|  |
|updateAction|ForeignKeyAction|ORM : Action to be applied to the foreign key for this element for action upon update|  |
|index|String|ORM : Name of any index constraint to add|  |
|indexed|String|ORM : Whether this element column is indexed|  |
|unique|String|ORM : Whether this element column is unique|  |
|uniqueKey|String|ORM : Name of any unique key constraint to add|  |
|columns|[Column](#Column)\[\]|ORM : Column definition for the column(s) of this element|  |
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

```java
@PersistenceCapable
public class MyClass
{
    @Element(types=mydomain.MyElementClass.class, dependent="true")
    Collection myField;
    ...
}
```

### @Order

Annotation used to define the ordering of an order-based Collection/array to be persisted. Maps across to the `<order>` MetaData element. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|mappedBy|String|ORM : Field in the element class that represents the ordering of the collection/array|  |
|column|String|ORM : Name of the column for this order|  |
|columns|[Column](#Column)\[\]|ORM : Column definition for the column(s) of this order|  |
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

```java
@PersistenceCapable
public class MyClass
{
    @Element(types=mydomain.MyElementClass.class, dependent="true")
    @Order(column="ORDER_IDX")
    Collection myField;
    ...
}
```

### @Key

Annotation used to define the key for any map to be persisted. Maps across to the `<map>` and `<key>` MetaData elements. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|types|Class\[\]|Type(s) of key.|When using generics will be taken from the Map definition, otherwise must be specified|
|embedded|String|Whether the key is embedded into a join table|  |
|serialized|String|Whether the key is serialised into the join table|  |
|dependent|String|Whether the key objects are dependent when deleting the owner map|  |
|mappedBy|String|Used to specify the field in the value class where the key is stored (optional).|  |
|embeddedMapping|[Embedded](#Embedded)\[\]|Definition of any embedding of the (persistable) key. Only 1 "Embedded" should be provided|  |
|table|String|ORM : Name of the table for this key|  |
|column|String|ORM : Name of the column for this key|  |
|foreignKey|String|ORM : Name of any foreign-key constraint to add|  |
|generateForeignKey|String|ORM : Whether to generate a FK constraint for the key (when not specifying the name)|  |
|deleteAction|ForeignKeyAction|ORM : Action to be applied to the foreign key for this key for action upon deletion|  |
|updateAction|ForeignKeyAction|ORM : Action to be applied to the foreign key for this key for action upon update|  |
|index|String|ORM : Name of any index constraint to add|  |
|indexed|String|ORM : Whether this key column is indexed|  |
|uniqueKey|String|ORM : Name of any unique key constraint to add|  |
|unique|String|ORM : Whether this key column is unique|  |
|columns|[Column](#Column)\[\]|ORM : Column definition for the column(s) of this key|  |
|extensions|[Extension](#Extension)\[\]|Vendor extensions|  |

```java
@PersistenceCapable
public class MyClass
{
    @Key(types=java.lang.String.class)
    Map myField;
    ...
}
```

### @Value

Annotation used to define the value for any map to be persisted. Maps across to the `<map>` and `<value>` MetaData elements. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|types |Class\[\]|Type(s) of value.|When using generics will be taken from the Map definition, otherwise must be specified|
|embedded|String|Whether the value is embedded into a join table|  |
|serialized|String|Whether the value is serialised into the join table|  |
|dependent | String | Whether the value objects are dependent when deleting the owner map |  |
| mappedBy | String | Used to specify the field in the key class where the value is stored (optional). |  |
| embeddedMapping |[Embedded](#Embedded)\[\] | Definition of any embedding of the (persistable) value. Only 1 "Embedded" should be provided |  |
| table | String |ORM : Name of the table for this value |  |
| column | String | ORM : Name of the column for this value |  |
| foreignKey | String | ORM : Name of any foreign-key constraint to add |  |
| deleteAction | ForeignKeyAction | ORM : Action to be applied to the foreign key for this value for action upon deletion |  |
| generateForeignKey | String | ORM : Whether to generate a FK constraint for the value (when not specifying the name)|  |
| updateAction | ForeignKeyAction | ORM : Action to be applied to the foreign key for this value for action upon update |  |
| index | String | ORM : Name of any index constraint to add |  |
| indexed | String | ORM : Whether this value column is indexed |  |
| uniqueKey | String | ORM : Name of any unique key constraint to add |  |
| unique | String | ORM : Whether this value column is unique |  |
| columns |[Column](#Column)\[\] | ORM : Column definition for the column(s) of this value |  |
| extensions |[Extension](#Extension)\[\] | Vendor extensions |  |

```java
@PersistenceCapable
public class MyClass
{
@Key(types=java.lang.String.class)
@Value(types=mydomain.MyValueClass.class, dependent="true")
Map myField;
...
}
```

### @Join

Annotation used to specify a join to a join table for a collection/array/map. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|table |String|ORM : Name of the table|  |
|column|String|ORM : Name of the column to join our PK to in the join table (when only one column used)|  |
|primaryKey|String|ORM : Name of any primary key constraint to add for the join table|  |
|generatePrimaryKey|String|ORM : Whether to generate a PK constraint on the join table (when not specifying the name)|  |
| foreignKey | String | ORM : Name of any foreign-key constraint to add |  |
| generateForeignKey | String | ORM : Whether to generate a FK constraint on the join table (when not specifying the name)|  |
| index | String | ORM : Name of any index constraint to add |  |
| indexed | String | ORM : Whether the join column(s) is indexed |  |
| uniqueKey | String | ORM : Name of any unique constraint to add |  |
| unique | String | ORM : Whether the join column(s) has a unique constraint |  |
| columns |[Column](#Column)\[\] | ORM : Name of the columns to join our PK to in the join table (when multiple columns used)|  |
| extensions |[Extension](#Extension)\[\] | Vendor extensions |  |

```java
@PersistenceCapable
public class MyClass
{
@Persistent
@Element(types=mydomain.MyElement.class)
@Join(table="MYCLASS\_ELEMENTS", column="MYCLASS\_ELEMENTS\_PK")
Collection myField;
...
}
```

### @Embedded

Annotation used to define that the field contents is embedded into the same table as this field Maps across to the `<embedded>` MetaData element. Specified on the **field/method**.


| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|ownerMember | String | ORM : The field/property in the embedded object that links back to the owning object (where it has a bidirectional relation)|  |
| nullIndicatorColumn | String | ORM : The column in the embedded object used to judge if the embedded object is null. |  |
| nullIndicatorValue | String | ORM : The value in the null column to interpret the object as being null. |  |
| members |[Persistent](#Persistent)\[\] | ORM : Field/property definitions for this embedding. |  |

```java
@PersistenceCapable
public class MyClass
{
@Embedded(members={
@Persistent(name="field1", columns=@Column(name="OTHER\_FLD\_1")),
@Persistent(name="field2", columns=@Column(name="OTHER\_FLD\_2"))
}
MyOtherClass myField;
...
}

@PersistenceCapable
@EmbeddedOnly
public class MyOtherClass
{
@Persistent
String field1;

    @Persistent
    String field2;
}
```

### @Columns

Annotation used to define the columns into which a field is persisted. If the field is persisted into a single column then @Column should be used. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value |[Column](#Column)\[\] | Array of columns - see @Columns annotation |  |

```java
@PersistenceCapable
public class MyClass
{
@Persistent
@Columns({@Column(name="RED"), @Column(name="GREEN"), @Column(name="BLUE"), @Column(name="ALPHA")})
Color myField;
...
}
```

### @Column

Annotation used to define that the colum where a field is persisted. Is equivalent to the `<column>` metadata element when specified under field. Specified on the **field/method** (and within other annotations).

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|name | String | ORM : Name of the column |  |
| target | String | ORM : Column in the other class that this maps to |  |
| targetMember | String | ORM : Field/Property in the other class that this maps to |  |
| jdbcType | String | ORM : JDBC Type to use for persisting into this column |  |
| sqlType | String | ORM : SQL Type to use for persisting into this column |  |
| length | int | ORM : Max length of data to store in this column |  |
| scale | int | ORM : Max number of floating points of data to store in this column |  |
| allowsNull | String | ORM : Whether null is allowed to be persisted into this column |  |
| defaultValue | String | ORM : Default value to persist into this column. If you want the default to be NULL, then put this as "#NULL"|  |
| insertValue | String | ORM : Value to insert into this column when it is an "unmapped" column. If you want the inserted value to be NULL, then put this as "#NULL"|  |
| position | int | Position of this column in the owning table (0 = first)|  |
| extensions |[Extension](#Extension)\[\] | Vendor extensions |  |

```java
@PersistenceCapable
public class MyClass
{
@Persistent
@Column(name="MYCOL", jdbcType="VARCHAR", length=40)
String field1;

    ...
}
```

### @Index

Annotation used to define that this field is indexed. Is equivalent to the `<index>` metadata element when specified under field. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|name | String | ORM : Name of the index |  |
| unique | String | ORM : Whether the index is unique |  |

```java
@PersistenceCapable
public class MyClass
{
@Persistent
@Index(name="MYFIELD1\_IDX")
String field1;

    @Persistent
    @Index(name="MYFIELD2\_IDX", unique="true")
    String field2;

    ...
}
```

### @Unique

Annotation used to define that this field has a unique constraint. Is equivalent to the `<unique>` metadata element when specified under field. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|name | String | ORM : Name of the constraint |  |
| deferred | String | ORM : Whether the constraint is deferred |  |

```java
@PersistenceCapable
public class MyClass
{
@Persistent
@Unique(name="MYFIELD1\_IDX")
String field1;

    ...
}
```

### @ForeignKey

Annotation used to define the foreign key for a relationship field. Is equivalent to the `<foreign-key>` metadata element when specified under field. Specified on the **field/method**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|name | String | ORM : Name of the constraint |  |
| deferred | String | ORM : Whether the constraint is deferred |  |
| unique | String | ORM : Whether the constraint is unique |  |
| deleteAction | ForeignKeyAction | ORM : Action to apply to the FK to be used on deleting | ForeignKeyAction.RESTRICT |
| updateAction | ForeignKeyAction | ORM : Action to apply to the FK to be used on updating | ForeignKeyAction.RESTRICT |

```java
@PersistenceCapable
public class MyClass
{
@Persistent
@ForeignKey(name="MYFIELD1\_FK", deleteAction=ForeignKeyAction.RESTRICT)
String field1;

    ...
}
```

### @Extensions

Annotation used to define a set of extensions specific to the JDO2 implementation being used. Specified on the **class** or **field**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|value |[Extension](#Extension)\[\] | Array of extensions - see @Extension annotation |  |

```java
@PersistenceCapable
@Extensions({@Extension(vendorName="MyJDOImpl", key="firstExtension", value="myValue"),
@Extension(vendorName="MyJDOImpl", key="secondExtension", value="myValue")})
public class Person
{
...
}
```

### @Extension

Annotation used to define an extension specific to a particular JDO implementation. Is equivalent to the `<extension>` metadata element. Specified on the **class** or **field**.

| Attribute | Type | Description | Default |
| --- | --- | --- | --- |
|vendorName | String | Name of the JDO vendor |  |
| key | String | Key for the extension |  |
| value | String | Value of the extension |  |

```java
@PersistenceCapable
@Extension(vendorName="MyJDOImpl", key="RunFast", value="true")
public class Person
{
...
}
```
