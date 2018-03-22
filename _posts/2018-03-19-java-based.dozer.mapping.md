---
layout: post
title:  "Java based Dozer mapping"
date:   2018-03-19 15:00:00 +0300
author: solairerove
categories: dozer java
---
To use Dozer add library due some dependency management

```xml
<!-- https://mvnrepository.com/artifact/net.sf.dozer/dozer -->
<dependency>
    <groupId>net.sf.dozer</groupId>
    <artifactId>dozer</artifactId>
    <version>5.5.1</version>
</dependency>
```

```gradle
// https://mvnrepository.com/artifact/net.sf.dozer/dozer
compile group: 'net.sf.dozer', name: 'dozer', version: '5.5.1'
```

Add java based Dozer configuration

```java
/**
 * Configuration for Dozer.
 */
@Configuration
@AllArgsConstructor(onConstructor = @__(@Autowired))
public class DozerConfig {

    private static final String PACKAGE_TO_SCAN = "path.to.bean.mappers.package";

    private final List<CustomConverter> customConverters;

    /**
     * Dozer bean mapper configuration.
     *
     * @return return configured spring bean.
     * @throws ReflectiveOperationException an exception.
     */
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

Than add necessary bean mappers

```java
/**
 * Mapping rules for Result to ResultResponse.
 */
public class Result2ResultResponse extends BeanMappingBuilder {

    @Override
    protected void configure() {
        mapping(Result.class, ResultResponse.class, TypeMappingOptions.oneWay())
                .fields("id", "id")
                .fields("status", "status")
                .fields("result", "result", copyByReference());
    }
}
```

create custom converter

create custom converter as spring bean