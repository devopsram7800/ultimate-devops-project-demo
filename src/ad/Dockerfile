FROM eclipse-temurin:21-jdk AS build
WORKDIR /usr/src/app/
COPY gradlew* build.gradle settings.gradle
COPY ./gradle ./
RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew  downloadRepos

COPY . .
RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto
ENV AD_PORT 9099

ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
