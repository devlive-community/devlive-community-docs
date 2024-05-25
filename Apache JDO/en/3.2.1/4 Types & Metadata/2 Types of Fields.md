[TOC]

### Supported Java Types

When persisting a class, a persistence solution needs to know how to persist the types of each field in the class. Clearly a persistence solution can only support a finite number of Java types. It cannot know how to persist every possible type creatable. The JDO specifications define lists of types that are required to be supported by all implementations of those specifications. This support can be conveniently split into two parts

- An object that can be referred-to (object reference, providing a relation) and that has an "identity" - **First Class Object (FCO)**. JDO requires an implementation to support PersistenceCapable types, as well as object/interface fields that refer to PersistenceCapable objects.

- An object that does not have an "identity" - **Second Class Object (SCO)**. This is something like a String or Date field in a class. It can also be a Collection, that contains other objects.

### First-Class (FCO) Types

JDO requires objects that are **PersistenceCapable** to be **FCO**. In addition it supports persisting fields of Interface or java.lang.Object type as FCO (since these are just references to PersistenceCapable objects).

### Second-Class (SCO) Types

The table below shows the supported **SCO** java types in JDO2. The table also shows the default-fetch-group (DFG) setting for that Java type (so whether it is retrieved by default when retrieving an object with a field of that type), whether the field is persisted by default (if it is "false" then you would have to add **persistence-modifier="persistent"** to the field for it to be persisted by JDO), and whether the java type can be used as part of the primary key.

#### Simple Types

The following "simple" types are supported by default by the JDO spec.

| Java Type                        | DFG? | Persistent? | PK? |
|----------------------------------|------|-------------|-----|
| boolean                          | ✅    | ✅           | ✅   |
| byte                             | ✅    | ✅           | ✅   |
| char                             | ✅    | ✅           | ✅   |
| double                           | ✅    | ✅           | ❌   |
| float                            | ✅    | ✅           | ❌   |
| int                              | ✅    | ✅           | ✅   |
| long                             | ✅    | ✅           | ✅   |
| short                            | ✅    | ✅           | ✅   |
| java.lang.Boolean                | ✅    | ✅           | ✅   |
| java.lang.Byte                   | ✅    | ✅           | ✅   |
| java.lang.Character              | ✅    | ✅           | ✅   |
| java.lang.Double                 | ✅    | ✅           | ❌   |
| java.lang.Float                  | ✅    | ✅           | ❌   |
| java.lang.Integer                | ✅    | ✅           | ✅   |
| java.lang.Long                   | ✅    | ✅           | ✅   |
| java.lang.Short                  | ✅    | ✅           | ✅   |
| java.lang.Number                 | ✅    | ✅           | ❌   |
| java.lang.Object                 | ❌    | ❌           | ❌   |
| java.lang.String                 | ✅    | ✅           | ✅   |
| java.math.BigDecimal             | ✅    | ✅           | ❌   |
| java.math.BigInteger             | ✅    | ✅           | ✅   |
| java.util.Currency               | ❌    | ✅           | ✅   |
| java.util.Locale                 | ❌    | ✅           | ✅   |
| java.lang.Enum                   | ✅    | ✅           | ✅   |
| java.lang.Optional               | ✅    | ✅           | ❌   |
| java.io.Serializable             | ❌    | ❌           | ❌   |
| javax.jdo.spi.PersistenceCapable | ❌    | ✅           | ✅   |

#### Temporal Types

The following temporal types are supported by default by the JDO spec.

| Java Type                | DFG? | Persistent? | PK? |
|--------------------------|------|-------------|-----|
| java.sql.Date            | ❌    | ❌           | ✅   |
| java.sql.Time            | ❌    | ❌           | ✅   |
| java.sql.Timestamp       | ❌    | ❌           | ✅   |
| java.util.Date           | ✅    | ✅           | ✅   |
| java.time.LocalDateTime  | ✅    | ✅           | ✅   |
| java.time.LocalTime      | ✅    | ✅           | ✅   |
| java.time.LocalDate      | ✅    | ✅           | ✅   |
| java.time.OffsetDateTime | ✅    | ✅           | ✅   |
| java.time.OffsetTime     | ✅    | ✅           | ✅   |
| java.time.MonthDay       | ✅    | ✅           | ✅   |
| java.time.YearMonth      | ✅    | ✅           | ✅   |
| java.time.Year           | ✅    | ✅           | ✅   |
| java.time.Period         | ✅    | ✅           | ✅   |
| java.time.Instant        | ✅    | ✅           | ✅   |
| java.time.Duration       | ✅    | ✅           | ✅   |
| java.time.ZoneId         | ✅    | ✅           | ✅   |
| java.time.ZoneOffset     | ✅    | ✅           | ✅   |
| java.time.ZonedDateTime  | ✅    | ✅           | ✅   |

#### Collection/Map Types

The following "container" types are supported by default by the JDO spec, subject to the JDO implementation supporting that feature.

| Java Type               | DFG? | Persistent? | PK? |
|-------------------------|------|-------------|-----|
| java.util.ArrayList     | ❌    | ✅           | ❌   |
| java.util.Collection    | ❌    | ✅           | ❌   |
| java.util.HashMap       | ❌    | ✅           | ❌   |
| java.util.HashSet       | ❌    | ✅           | ❌   |
| java.util.Hashtable     | ❌    | ✅           | ❌   |
| java.util.LinkedHashMap | ❌    | ✅           | ❌   |
| java.util.LinkedHashSet | ❌    | ✅           |     |
| java.util.LinkedList    | ❌    | ✅           | ❌   |
| java.util.List          | ❌    | ✅           | ❌   |
| java.util.Map           | ❌    | ✅           | ❌   |
| java.util.Set           | ❌    | ✅           | ❌   |
| java.util.TreeMap       | ❌    | ✅           | ❌   |
| java.util.TreeSet       | ❌    | ✅           | ❌   |
| java.util.Vector        | ❌    | ✅           | ❌   |

#### Array Types

The vast majority of the "simple" SCO types can also be persisted as arrays of that type as well.


| Java Type                            | DFG? | Persistent? | PK? |
|--------------------------------------|------|-------------|-----|
| boolean\[\]                          | ❌    | ✅           | ❌   |
| byte\[\]                             | ❌    | ✅           | ❌   |
| char\[\]                             | ❌    | ✅           | ❌   |
| double\[\]                           | ❌    | ✅           | ❌   |
| float\[\]                            | ❌    | ✅           | ❌   |
| int\[\]                              | ❌    | ✅           | ❌   |
| long\[\]                             | ❌    | ✅           | ❌   |
| short\[\]                            | ❌    | ✅           | ❌   |
| java.lang.Boolean\[\]                | ❌    | ✅           | ❌   |
| java.lang.Byte\[\]                   | ❌    | ✅           | ❌   |
| java.lang.Character\[\]              | ❌    | ✅           | ❌   |
| java.lang.Double\[\]                 | ❌    | ✅           | ❌   |
| java.lang.Float\[\]                  | ❌    | ✅           | ❌   |
| java.lang.Integer\[\]                | ❌    | ✅           | ❌   |
| java.lang.Long\[\]                   | ❌    | ✅           | ❌   |
| java.lang.Short\[\]                  | ❌    | ✅           | ❌   |
| java.lang.String\[\]                 | ❌    | ✅           | ❌   |
| java.math.BigDecimal\[\]             | ❌    | ✅           | ❌   |
| java.math.BigInteger\[\]             | ❌    | ✅           | ❌   |
| java.util.Date\[\]                   | ❌    | ✅           | ❌   | 
| java.util.Locale\[\]                 | ❌    | ✅           | ❌   | 
| java.lang.Enum\[\]                   | ❌    | ✅           | ❌   | 
| javax.jdo.spi.PersistenceCapable\[\] | ❌    | ✅           | ❌   |

### JDO Attribute Converters

JDO3.2 introduces an API for conversion of an attribute of a PersistenceCapable object to its datastore value. You can define a "converter" that will convert to the datastore value and back from it, implementing this interface. This is particularly useful where you have a field type that would not normally be readily persistable, but by defining the conversion it becomes simple.

```java
public interface AttributeConverter<X,Y>
{
    public Y convertToDatastore(X attributeValue);

    public X convertToAttribute (Y datastoreValue);
}
```

so if we have a simple converter to allow us to persist fields of type URL in a String form in the datastore, like this

```java
public class URLStringConverter implements AttributeConverter<URL, String>
{
    public URL convertToAttribute(String str)
    {
        if (str == null)
        {
            return null;
        }

        URL url = null;
        try
        {
            url = new java.net.URL(str.trim());
        }
        catch (MalformedURLException mue)
        {
            throw new IllegalStateException("Error converting the URL", mue);
        }
        return url;
    }

    public String convertToDatastore(URL url)
    {
        return url != null ? url.toString() : null;
    }
}
```

and now in our PersistenceCapable class we mark any URL field as being converted using this converter

```java
@PersistenceCapable
public class MyClass
{
    @PrimaryKey
    long id;

    @Convert(URLStringConverter.class)
    URL url;

    ...
}
```

or using XML metadata

```xml
<field name="url" converter="mydomain.package.URLStringConverter"/>
```

A further use of **AttributeConverter** is where you want to apply type conversion to the key/value of a Map field, or to the element of a Collection field. The Collection element case is simple, you just specify the @Convert against the field and it will be applied to the element. If you want to apply type conversion to a key/value of a map do this.

```java
@Key(converter=URLStringConverter.class)
Map<URL, OtherEntity> myMap;
```

or using XML metadata

```xml
<field name="myMap">
    <key converter="mydomain.package.URLStringConverter"/>
</field>
```

> You can register a default `AttributeConverter` for a java type when constructing the PMF via persistence properties. These properties should be of the form **javax.jdo.option.typeconverter.{javatype}** and the value is the class name of the `AttributeConverter`.

> You CANNOT use an `AttributeConverter` for a PersistenceCapable type. This is because a PersistenceCapable type requires special treatment, such as attaching a StateManager etc.

> The `AttributeConverter` objects shown here are **stateless**.
