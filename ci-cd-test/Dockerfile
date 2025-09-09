# Build stage
FROM gradle:8.10-jdk21 AS builder
WORKDIR /app
COPY . .
# ✅ 추가: gradlew 실행권한 부여
RUN chmod +x gradlew
#RUN ./gradlew clean bootJar --no-daemon
# ✅ 일반 자바 프로젝트: jar 빌드
RUN ./gradlew clean build --no-daemon

# Run stage
FROM eclipse-temurin:21-jre
WORKDIR /app
#COPY --from=builder /app/app/build/libs/app.jar app.jar
# ✅ 빌드 산출물 복사 (이름 가변 → *.jar)
COPY --from=builder /app/build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]
