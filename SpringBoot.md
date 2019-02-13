# SpringBoot

## How do I return custom status codes?

## How do I deploy my application?

- `./gradlew build`
- find the `build/libs/[artifact-name].jar`
- run `java -jar [artifact-name].jar` in the terminal
  - or find the jar and double click on it (it'll be hard to kill this process this way)

## How do I deploy with Docker?

Example Dockerfile

```
FROM java:8
EXPOSE 8080
ADD /build/libs/service-0.0.1-SNAPSHOT.jar service.jar
ENTRYPOINT ["java", "-jar", "service.jar"]
```

## How do I access environment variables in my app?

### Simple Kotlin Solution

- `System.getEnv('[variable name]')`
- toggle configuration based on this

## How do I use \*.properties files with Kotlin (Spring Classes Only)

- add `annotationProcessor "org.springframework.boot:spring-boot-configuration-processor"` to gradle dependencies
- add a new class to house your properties

```
@ConfigurationProperties(prefix = "service")
class ServiceProperties {
    lateinit var property: String
}
```

- register the properties class in the application class

```
@EnableConfigurationProperties(ServiceProperties::class)
class ServiceApplication
```

- inject the properties object into the class that needs it

```
class GreetingController(private val properties: ServiceProperties) {
```

- use the properties object as normal

```
properties.property
```

## How do I use \*.properties files with Kotlin

after starting the application context

```
val appContext = SpringApplication.run(ServiceApplication::class.java, *args)
```

get a copy of your peropeties bean/class

```
val config = appContext.getBean(ServiceProperties::class.java)
```

then access the props as above

```
System.out.println("Running Service In Environment: ${config.environment}")
```

## Environment Specific Config

- create a new \*.properties file
- give it a name matching `application-*profile*.properties`
- now when the app is run with `*profile*` via an IDE or command line, the props in `application-*profile*.properties` will apply
