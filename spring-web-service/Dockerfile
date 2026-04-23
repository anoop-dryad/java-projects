FROM amazoncorretto:26 AS build
WORKDIR /app
RUN yum install -y maven
COPY pom.xml  /app/.
RUN mvn dependency:go-offline
COPY . .
RUN mvn clean package -DskipTests


FROM amazoncorretto:26 AS run
WORKDIR /app
COPY --from=build /app/target/*.jar /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
