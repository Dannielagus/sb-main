
FROM alpine/git as git-clone
WORKDIR /app
RUN git clone https://github.com/Dannielagus/sb-user.git sb-user

FROM maven:3.6.1-jdk-8-alpine as app-build
WORKDIR /app
COPY --from=git-clone /app/sb-user /app
RUN mvn install -DskipTests

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=app-build /app/target/user-service.jar /app
EXPOSE 8001
ENTRYPOINT ["java", "-jar", "user-service.jar"]
