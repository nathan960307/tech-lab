# 🧪 Tech Lab
새로운 기술들을 실험하고 학습한 내용을 정리하는 공간입니다.
각 실험은 폴더별로 구성되어 있으며, 진행 과정과 트러블슈팅을 기록합니다.

## 📂 실험 기록

- [ ] CI/CD Test (2025-09-08 ~ 2025-09-09)
  <details>
      <summary>상세 보기</summary>
    
      ### 🎯 목표
      - GitHub Actions로 Gradle 빌드 + 테스트 자동화 실습
  
      ### 🛠 진행 순서
      1. `gradle init`으로 Java 프로젝트 생성 (JDK 21, Groovy DSL, JUnit Jupiter)
      2. 프로젝트를 `ci-cd-test/` 폴더로 이동
      3. `.gitignore` 정리 (build/, .gradle/, .idea/ 등 제외)
      4. GitHub에 push & Issue #1 연결
      5. `.github/workflows/ci.yml` 생성 → build/test 실행
      
      ### ⚠ 트러블슈팅
      - **Gradle 설치/설정 문제**
      - 증상: 초기 환경에 Gradle 설치 여부 확인 필요
      - 해결: `gradle -v` → 8.14.2 버전 확인 완료, 설치 불필요
      
      ### ✅ 현재 상태
      - GitHub Actions CI 파이프라인 적용 완료
      - push/pull_request 이벤트 시 자동 빌드 & 테스트 실행
      
  </details>
- [ ] Redis Test (2025-09-00 ~ 2025-09-00)
- [ ] ElasticSearch (2025-09-00 ~ 2025-09-00)
- [ ] Kafka Test (2025-09-00 ~ 2025-09-00)
- [ ] Spring Batch (2025-09-00 ~ 2025-09-00)


## 🚀 목적
- 기술별 미니 프로젝트를 통해 핵심 개념 학습
- 실패/트러블슈팅 내역 기록
- 이후 포트폴리오/실무 적용에 참고
