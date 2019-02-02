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
