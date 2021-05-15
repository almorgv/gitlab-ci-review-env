FROM gradle:6.8-jdk11 as builder
COPY . /app
WORKDIR /app
ENV GRADLE_OPTS -Dkotlin.compiler.execution.strategy="in-process"
ENV JAVA_OPTS -XX:-UsePerfData
RUN gradle --no-daemon build

RUN addgroup app && adduser --ingroup app --disabled-password app
USER app

FROM nxrm:18443/distroless/java:11
COPY --from=builder /app/build/libs/*.jar /app/app.jar
WORKDIR /app
ENTRYPOINT ["java", "-jar", "app.jar"]
