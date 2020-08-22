
FROM alpine/git as git-clone
WORKDIR /app
RUN git clone https://github.com/Dannielagus/sb-supplier.git sb-supplier

FROM maven:3.6.1-jdk-8-alpine as app-build
WORKDIR /app
COPY --from=git-clone /app/sb-supplier /app
RUN mvn install -DskipTests

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=app-build /app/target/supplier-service.jar /app
EXPOSE 8001
ENTRYPOINT ["java", "-jar", "supplier-service.jar"]
