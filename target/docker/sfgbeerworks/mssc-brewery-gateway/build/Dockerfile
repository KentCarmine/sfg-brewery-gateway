FROM openjdk:11-jre-slim as builder
WORKDIR application
ADD maven/mssc-brewery-gateway-1.0-SNAPSHOT.jar mssc-brewery-gateway-1.0-SNAPSHOT.jar
RUN java -Djarmode=layertools -jar mssc-brewery-gateway-1.0-SNAPSHOT.jar extract

FROM openjdk:11-jre-slim
LABEL PROJECT_NAME=mssc-brewery-gateway \
      PROJECT=com.github.sfg-beer-works:mssc-brewery-gateway:jar:1.0-SNAPSHOT

EXPOSE 8080

WORKDIR application
COPY --from=builder application/dependencies/ ./
COPY --from=builder application/spring-boot-loader/ ./
COPY --from=builder application/snapshot-dependencies/ ./
COPY --from=builder application/application/ ./
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "org.springframework.boot.loader.JarLauncher"]
