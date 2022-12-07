# define args
ARG VERSION_NUM=1.0.0

#build stage.
FROM maven:3 as build_stage 
WORKDIR /my-app
COPY . .
RUN mvn -B compile -e -f pom.xml

#package stage.
FROM build_stage AS package_stage
WORKDIR /my-app
RUN mvn -B package -e -f pom.xml

#app stage
FROM openjdk:11-jdk-slim AS app_stage
WORKDIR /my-app
ENV VERSION_NUM=${VERSION_NUM}
COPY --from=package_stage target/my-app-${VERSION_NUM}.jar ${HOME_PATH_ON_IMAGE}
#CMD java -jar my-app-*.jar
CMD ["/usr/bin/java", "-jar", "my-app-1.0.0.jar"]