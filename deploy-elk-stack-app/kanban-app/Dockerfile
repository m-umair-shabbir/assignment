FROM maven:3.6.1-jdk-8-slim AS build
RUN mkdir -p /workspace
WORKDIR /workspace
COPY pom.xml /workspace
COPY src /workspace/src
RUN mvn -f pom.xml clean package
ADD https://artifacts.elastic.co/downloads/logstash/logstash-7.9.0.tar.gz /logstash
COPY logstash-nignx.conf /logstash-nignx.conf
#RUN /logstash/bin/logstash -f /logstash-nignx.conf
FROM openjdk:8-alpine
COPY --from=build /workspace/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
