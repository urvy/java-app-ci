FROM openjdk:17-jdk-slim
COPY target/*.jar /app/myapp.jar
WORKDIR /app
ENTRYPOINT ["java", "-jar", "myapp.jar"]
