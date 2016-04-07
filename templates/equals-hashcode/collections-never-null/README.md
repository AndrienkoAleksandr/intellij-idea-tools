Here you can find the `equals` and `hashCode` templates for POJOs
which getters never return null where collection/map is expected.

A few things to know:
- Generated code fits [google java style](https://google.github.io/styleguide/javaguide.html)
- The templates don't respect the _Generate hashCode & equals_ wizard options(except of selected class fields)
- How to add the templates using the [templates dialog](https://www.jetbrains.com/help/idea/2016.1/templates-dialog.html?origin=old_help)
- Generated code is `java8+` compatible

For the class:

```java

public class Example {

    private char                charVal;
    private byte                byteVal;
    private short               shortVal;
    private int                 intVal;
    private long                longVal;
    private float               floatVal;
    private double              doubleVal;
    private boolean             booleanVal;
    private String[]            array;
    private String              string;
    private Map<String, String> map;
    private List<String>        list;

    // ...

    public Map<String, String> getMap() {
        if (map == null) {
            map = new HashMap<>();
        }
        return map;
    }

    public List<String> getList() {
        if (list == null) {
            list = new ArrayList<>();
        }
        return list;
    }

    // ...

```

Generated equals is:

```java
@Override
public boolean equals(Object obj) {
    if (this == obj) {
        return true;
    }
    if (!(obj instanceof TestObject)) {
        return false;
    }
    final TestObject that = (TestObject)obj;
    return charVal == that.charVal
           && byteVal == that.byteVal
           && shortVal == that.shortVal
           && intVal == that.intVal
           && longVal == that.longVal
           && Float.compare(floatVal, that.floatVal) == 0
           && Double.compare(doubleVal, that.doubleVal) == 0
           && booleanVal == that.booleanVal
           && Arrays.equals(array, that.array)
           && Objects.equals(string, that.string)
           && getMap().equals(that.getMap())
           && getList().equals(that.getList());
}
```

Generated hashCode is:

```java
@Override
public int hashCode() {
    int hash = 7;
    hash = 31 * hash + charVal;
    hash = 31 * hash + byteVal;
    hash = 31 * hash + shortVal;
    hash = 31 * hash + intVal;
    hash = 31 * hash + Long.hashCode(longVal);
    hash = 31 * hash + Float.hashCode(floatVal);
    hash = 31 * hash + Double.hashCode(doubleVal);
    hash = 31 * hash + Boolean.hashCode(booleanVal);
    hash = 31 * hash + Arrays.hashCode(array);
    hash = 31 * hash + Objects.hashCode(string);
    hash = 31 * hash + getMap().hashCode();
    hash = 31 * hash + getList().hashCode();
    return hash;
}
```
