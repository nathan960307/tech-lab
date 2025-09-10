# 🧪 Tech Lab
새로운 기술들을 실험하고 학습한 내용을 정리하는 공간입니다.
각 실험은 폴더별로 구성되어 있으며, 진행 과정과 트러블슈팅을 기록합니다.

## 📂 실험 기록

- [ ] CI/CD Test (2025-09-08 ~ 2025-09-09)
  <details>
      <summary>상세 보기</summary>
    
      ### 🎯 목표
      - GitHub Actions로 Gradle 빌드 + 테스트 + Docker 이미지 빌드 & 푸시 자동화 실습
      - Docker Hub → GCP VM 자동 배포(CD) 플로우 검증
  
      ### 🛠 진행 순서
      #### CI
      1. `gradle init`으로 Java 프로젝트 생성 (JDK 21, Groovy DSL, JUnit Jupiter)
      2. 프로젝트를 `ci-cd-test/` 폴더로 이동
      3. `.gitignore` 정리 (build/, .gradle/, .idea/ 등 제외)
      4. GitHub에 push & Issue #1 연결
      5. `.github/workflows/ci.yml` 생성 → build/test 실행
      6. `Dockerfile` + `.dockerignore` 작성
      7. GitHub Secrets (`DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`) 추가
      8. Docker Hub 리포지토리(`nathan9603/tech-lab`) 생성 및 푸시 설정
      9. CI 실행 확인 → `latest`, `0.0.1`, `YYYYMMDD-<commitSHA>` 태그로 이미지 업로드 완료
      #### CD
      1. GCP VM 생성 (e2-medium, Debian 12) 및 방화벽 규칙(8080, 22) 설정
      2. 로컬에서 SSH 키 생성(`id_rsa`, `id_rsa.pub`) 후 GCP Metadata에 등록
      3. GitHub Secrets (`GCP_VM_HOST`, `GCP_VM_USER`, `GCP_SSH_KEY`) 추가
      4. `.github/workflows/cd.yml` 생성 → appleboy/ssh-action으로 원격 배포 자동화
      5. CD 실행 시
       - 최신 이미지 pull
       - 기존 컨테이너 stop & rm
       - 새 컨테이너 run (-p 8080:8080)
      
      ### ⚠ 트러블슈팅
      - **gradlew 실행 권한 문제**
        - 증상: Docker 빌드 중 `/bin/sh: 1: ./gradlew: Permission denied`
        - 해결: `RUN chmod +x gradlew` 추가하여 해결
      
       - **bootJar 태스크 없음**
        - 증상: `Task 'bootJar' not found`
        - 해결: 순수 Java 프로젝트라 `build` 사용 + `COPY --from=builder /app/build/libs/*.jar app.jar` 로 변경

      - **SSH 인증 실패**
        - 증상: `ssh.ParsePrivateKey: ssh: no key found`
        - 원인: GitHub Secrets에 개인키를 한 줄로 붙여넣음
        - 해결: 줄바꿈 포함 전체 개인키를 `GCP_SSH_KEY`에 다시 저장

      - **JAR 실행 실패 (no main manifest attribute)**
        - 증상: 컨테이너 실행 직후 종료
        - 원인: 일반 Java JAR에는 `Main-Class` 속성이 없음
        - 해결: `build.gradle`에 `jar { manifest { attributes('Main-Class': application.mainClass) } }` 추가 
      
      ### ✅ 현재 상태
      - CI 파이프라인: 빌드 & 테스트 성공 시 Docker 이미지 자동 생성 및 Docker Hub 푸시
      - Docker Hub: `latest`, `YYYYMMDD-<commitSHA>` 태그로 이미지 업로드 확인 완료
      
  </details>
- [ ] Redis Test (2025-09-00 ~ 2025-09-00)
- [ ] ElasticSearch (2025-09-00 ~ 2025-09-00)
- [ ] Kafka Test (2025-09-00 ~ 2025-09-00)
- [ ] Spring Batch (2025-09-00 ~ 2025-09-00)


## 🚀 목적
- 기술별 미니 프로젝트를 통해 핵심 개념 학습
- 실패/트러블슈팅 내역 기록
- 이후 포트폴리오/실무 적용에 참고
