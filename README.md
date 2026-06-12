# NSIGHT Marketing Platform Environment Config

## 구성 목적
단일 도메인 `nh.marketing.com` 기준으로 Apache, Tomcat, Spring Boot 설정을 통합한 샘플 환경파일입니다.

## 아키텍처
```text
nh.marketing.com
  ↓
Apache
  ├─ /customer  → customer-service Tomcat Cluster
  ├─ /campaign  → campaign-service Tomcat Cluster
  ├─ /event     → event-service Tomcat Cluster
  ├─ /support   → support-service Tomcat Cluster
  └─ /platform  → platform-service Tomcat Cluster

All Spring Services
  ↓
Spring Session Redis
```

## 핵심 원칙
- Apache: URL Prefix 기반 라우팅
- Tomcat: 서비스별 WAR/Context 배포
- Session: Tomcat DeltaManager 미사용, Spring Session Redis 사용
- Cookie: `NSIGHTSESSION`, Path `/`
- Domain: `nh.marketing.com`

## 반영 시 확인
- IP/Port는 실제 서버 기준으로 변경
- SSL 인증서 경로 변경
- Redis Sentinel/Cluster 사용 시 Spring Redis 설정 보강
- 운영 반영 전 `apachectl configtest`, `catalina.sh configtest`, Spring Boot 기동 테스트 수행
