# Build stage
FROM gradle:8.10-jdk21 AS builder
WORKDIR /app
COPY . .
# ✅ 추가: gradlew 실행권한 부여
RUN chmod +x gradlew
RUN ./gradlew clean bootJar --no-daemon

# Run stage
FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=builder /app/app/build/libs/app.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]
