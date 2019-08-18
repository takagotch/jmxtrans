### jmxtrans
---
https://github.com/jmxtrans/jmxtrans/

```java
// jmxtrans-core/src/test/java/com/googlecode/jmxtrans/JmxResultProcessorTest.java

public class JmxResultProcessorTest {
  private final static String TEST_DOMAIN_NAME = "ObjectDomainName";
  
  @Test
  public void canCreateBasicResultData() throws MalformedObjectNameException, InstanceNotFoundException {
    Attribute integerAttribute = new Attribute("StartTime", 51L);
    ObjectInstance runtime = getRuntime();
    List<Result> results = new JmxResultProcessor(
      dummyQueryWithResultAlias(),
      runtime,
      ImmutableList.of(integerAttribute),
      runtime.getClassName(),
      TEST_DOMAIN_NAME).getResults();
    
    assertThat(results).hasSize(1);
    Result integerResult = results.get(0);
    
    assertThat(integerResult.getAttributeName()).isEqualTo("StartTime");
    assertThat(integerResult.getClassName()).isEqualTo("sun.management.RuntimeImpl");
    assertThat(integerResult.getKeyAlias()).isEqualTo("resultAlias");
    assertThat(integerResult.getTypeName()).isEqualTo("type=Runtime");
    assertThat(integerResult.getValue()).isEqualTo(51L);
  }
  
  @Test
  public void doesNotReorderTypeNames() throws MalformedObjectNameException {
    String className = "java.lang.SomeClass";
    String propertiesOutOfOrder = "z-key=z-value,a-key=a-value,k-key=k-value";
    List<Result> results = new JmxResultProcessor(
      dummyQueryWithResultAlias(),
      new ObjectInstance(className + ":" + propertiesOutOfOrder, className),
      ImmutableList.of(new Attribute("SomeAttribute", 1)),
      className,
      TEST_DOMAIN_NAME).getResults();
    
    assertThat(results).hasSize(1);
    Result integerResult = results.get(0);
    assertThat(integerResult.getTypeName()).isEqualTo(propertiesOutOfOrder);
  }
  
  
  
}

```

```
```

```
```


