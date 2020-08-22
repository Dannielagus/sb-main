
FROM alpine/git as git-clone
WORKDIR /app
RUN git clone https://github.com/Dannielagus/sb-server.git sb-server

FROM maven:3.6.1-jdk-8-alpine as app-build
WORKDIR /app
COPY --from=git-clone /app/sb-server /app
RUN mvn install -DskipTests

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=app-build /app/target/eureka-server.jar /app
EXPOSE 8000
ENTRYPOINT ["java", "-jar", "eureka-server.jar"]
