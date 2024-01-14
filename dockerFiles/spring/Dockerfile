FROM docker.io/gradle:jdk17-focal as build
WORKDIR /app
COPY ./MineralIdentificationService /app/
RUN /app/gradlew build --stacktrace

#### Stage 2: A minimal docker image with command to run the app 
FROM docker.io/library/openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/build/libs /app/
RUN mkdir /images
ENTRYPOINT [ "java", "-jar", "MineralIdentificationService-0.0.1-SNAPSHOT.jar" ]