---
layout: post
title:  "Java based Dozer mapping"
date:   2018-07-13 15:29:00 +0300
author: solairerove
categories: dozer java
---
Full application is on this [headstone-dozer](https://github.com/LostIzalith/headstone-dozer) repository on GitHub.

To use Dozer add library due some dependency management:

```xml
<!-- https://mvnrepository.com/artifact/net.sf.dozer/dozer -->
<dependency>
    <groupId>net.sf.dozer</groupId>
    <artifactId>dozer</artifactId>
    <version>5.5.1</version>
</dependency>
```

```gradle
compile('net.sf.dozer:dozer:5.5.1')
```

Add java based Dozer configuration:

```java
@Configuration
public class DozerConfig {

    private static final String PACKAGE_TO_SCAN = "com.lost.izalith.headstone.dozer.mapping";

    @Bean
    public DozerBeanMapper mapper() throws ReflectiveOperationException {
        final DozerBeanMapper mapper = new DozerBeanMapper();
        final List<BeanMappingBuilder> registeredMapping = getRegisteredMappings();
        registeredMapping.forEach(mapper::addMapping);

        return mapper;
    }

    private List<BeanMappingBuilder> getRegisteredMappings() throws ReflectiveOperationException {
        final ClassPathScanningCandidateComponentProvider scanner = new ClassPathScanningCandidateComponentProvider(false);
        scanner.addIncludeFilter(new AssignableTypeFilter(BeanMappingBuilder.class));

        final List<BeanMappingBuilder> customMapping = new ArrayList<>();
        for (final BeanDefinition bd : scanner.findCandidateComponents(PACKAGE_TO_SCAN)) {
            customMapping.add((BeanMappingBuilder) Class.forName(bd.getBeanClassName()).newInstance());
        }
        return customMapping;
    }
}
```

Than add necessary bean mappers:

```java
public class SimpleRequest2SimpleEntity extends BeanMappingBuilder {

    @Override
    protected void configure() {
        mapping(HeadstoneSimpleRequest.class, HeadstoneSimpleEntity.class, TypeMappingOptions.oneWay())
                .fields("name", "name")
                .fields("key", "key")
                .fields("value", "value");
    }
}
```

```java
public class SimpleEntity2SimpleResponse extends BeanMappingBuilder {

    @Override
    protected void configure() {
        mapping(HeadstoneSimpleEntity.class, HeadstoneSimpleResponse.class, TypeMappingOptions.oneWay())
                .fields("name", "awesomeName")
                .fields("key", "key")
                .fields("value", "value");
    }
}
```

Some simple endpoint for example:

```java
@RestController
@RequestMapping("/headstone")
@RequiredArgsConstructor(onConstructor = @__(@Autowired))
public class HeadstoneController {

    private final DozerBeanMapper dozerBeanMapper;

    @PostMapping("/request")
    public ResponseEntity<HeadstoneSimpleResponse> whateverIWantPost(
            final @Valid @RequestBody HeadstoneSimpleRequest simpleRequest,
            final UriComponentsBuilder uriComponentsBuilder) {

        final UriComponents uriComponents = uriComponentsBuilder.path("/headstone/request").build();

        final HeadstoneSimpleEntity simpleEntity = dozerBeanMapper.map(simpleRequest, HeadstoneSimpleEntity.class);

        final HeadstoneSimpleResponse response = dozerBeanMapper.map(simpleEntity, HeadstoneSimpleResponse.class);

        return ResponseEntity.created(uriComponents.toUri())
                .contentType(MediaType.APPLICATION_JSON_UTF8)
                .body(response);
    }
}
```

Now lets send request to endpoint:

```http
POST /headstone/request HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Cache-Control: no-cache

{
	"name": "some name",
	"key": "uuid",
	"value": "lol"
}
```

Dozer allow to use custom converters, for example to convert string to enum and etc. 
So here's new custom converter:

```java
@Component
public class SomeEnumConverter implements CustomConverter {

    @Override
    public Object convert(final Object existingDestinationFieldValue,
                          final Object sourceFieldValue,
                          final Class<?> destinationClass,
                          final Class<?> sourceClass) {

        return Optional.ofNullable(sourceFieldValue)
                .map(e -> SomeEnum.ITEMS
                        .stream()
                        .filter(x -> x.getClientValue().equalsIgnoreCase(e.toString()))
                        .findAny()
                        .orElseThrow(() -> new IllegalArgumentException("Incorrect enum value " + e + ". "
                                + "Possible values are " + SomeEnum.ITEMS)))
                .orElse(null);
    }
}
``` 

And change config a little:

```java
@Configuration
@RequiredArgsConstructor(onConstructor = @__(@Autowired))
public class DozerConfig {

    private static final String PACKAGE_TO_SCAN = "com.lost.izalith.headstone.dozer.mapping";

    private final List<CustomConverter> customConverters;

    @Bean
    public DozerBeanMapper mapper() throws ReflectiveOperationException {
        final DozerBeanMapper mapper = new DozerBeanMapper();
        final List<BeanMappingBuilder> registeredMapping = getRegisteredMappings();
        registeredMapping.forEach(mapper::addMapping);

        final HashMap<String, CustomConverter> converters = new HashMap<>(getCustomConvertersWithId());
        mapper.setCustomConvertersWithId(converters);

        return mapper;
    }

    private List<BeanMappingBuilder> getRegisteredMappings() throws ReflectiveOperationException {
        final ClassPathScanningCandidateComponentProvider scanner = new ClassPathScanningCandidateComponentProvider(false);
        scanner.addIncludeFilter(new AssignableTypeFilter(BeanMappingBuilder.class));

        final List<BeanMappingBuilder> customMapping = new ArrayList<>();
        for (final BeanDefinition bd : scanner.findCandidateComponents(PACKAGE_TO_SCAN)) {
            customMapping.add((BeanMappingBuilder) Class.forName(bd.getBeanClassName()).newInstance());
        }
        return customMapping;
    }

    private Map<String, CustomConverter> getCustomConvertersWithId() {
        final Map<String, CustomConverter> customConverterMap = new HashMap<>();
        customConverters
                .forEach(converter -> customConverterMap.put(converter.getClass().getSimpleName(), converter));

        return customConverterMap;
    }
}
```

Add enum field in entity and string field in request:

```java
@Data
public class HeadstoneSimpleRequest {

    private String name;

    private String key;

    private String value;

    private String someEnum;
}
```

```java
@Data
public class HeadstoneSimpleEntity {

    private String name;

    private String key;

    private String value;

    private SomeEnum someEnum;
}
```

Next step is change mapper a little:

```java
public class SimpleRequest2SimpleEntity extends BeanMappingBuilder {

    @Override
    protected void configure() {
        mapping(HeadstoneSimpleRequest.class, HeadstoneSimpleEntity.class, TypeMappingOptions.oneWay())
                .fields("name", "name")
                .fields("key", "key")
                .fields("value", "value")
                .fields("someEnum", "someEnum", FieldsMappingOptions.customConverter(SomeEnumConverter.class));
    }
}
```

And all is work fine:

```http
POST /headstone/request HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Cache-Control: no-cache

{
	"name": "some name",
	"key": "uuid",
	"value": "lol",
	"someEnum": "start"
}
```

Now, lets create custom converter and inject some other bean into it.
Here's service:

```java
@Service
public class MyAwesomeService {

    public String awesomeString() {
        return "My awesome string";
    }
}
```

Here's brand new custom converter:

```java
@Component
@RequiredArgsConstructor(onConstructor = @__(@Autowired))
public class MyAwesomeCustomConverter implements CustomConverter {

    private final MyAwesomeService myAwesomeService;

    @Override
    public Object convert(final Object existingDestinationFieldValue,
                          final Object sourceFieldValue,
                          final Class<?> destinationClass,
                          final Class<?> sourceClass) {

        return myAwesomeService.awesomeString();
    }
}
```

And, as expected, using in mapper:

```java
public class SimpleRequest2SimpleEntity extends BeanMappingBuilder {

    @Override
    protected void configure() {
        mapping(HeadstoneSimpleRequest.class, HeadstoneSimpleEntity.class, TypeMappingOptions.oneWay())
                .fields("name", "name")
                .fields("key", "key")
                .fields("value", "value")
                .fields("someEnum", "someEnum", FieldsMappingOptions.customConverter(SomeEnumConverter.class))
                .fields("dataString", "myAwesomeString", customConverterId(
                        MyAwesomeCustomConverter.class.getSimpleName()
                ));
    }
}
```

And all is work fine:

```http
POST /headstone/request HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Cache-Control: no-cache

{
	"name": "some name",
	"key": "uuid",
	"value": "lol",
	"someEnum": "start"
}
```

With response:

```json
{
    "key": "uuid",
    "value": "lol",
    "someAction": "START",
    "myAwesomeString": "My awesome string",
    "name": "some name"
}
```
