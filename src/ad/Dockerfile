FROM eclipse-temurin:21-jdk AS build

WORKDIR /usr/src/app/


COPY gradlew* build.gradle settings.gradle* .
COPY ./gradle ./gradle
RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew  downloadRepos

COPY . .
COPY ./pb/ ./proto
RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto

FROM eclipse-temurin:21-jre
WORKDIR /usr/src/app/
COPY --from=build /usr/src/app/ ./
ENV AD_PORT 9099

ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
