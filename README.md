# 🚀 클라우드 네이티브 인프라 구축 프로젝트

## 📋 프로젝트 개요

<div align="center">
  <img src="https://github.com/user-attachments/assets/23387b63-6b8c-43ef-ace0-8e07f2d4ef69" alt="프로젝트 개요" style="max-width: 100%; height: auto;">
</div>

현재 시대의 SNS에서 **물질적 과시**가 만연한 상황과 이로 인해 발생하는 **다양한 문제점들**(낮은 자존감 및 끊임없는 자기비교)을 주목하여, **우리의 행복은 우리가 가진 것이 아니라, 우리의 존재 그 자체에서 나온다**는 컨셉을 모티브로 한 건강한 SNS 플랫폼을 구축했습니다.

### 🎯 주요 기능
- 개인 맞춤 **아바타** 생성 (웹툰 생성에 활용)
- 일기 작성 및 **AI 위로 코멘트**
- 일기 기반 **웹툰 및 음악** 생성 (음악 장르 선택 가능)
- 일기 **공유** 서비스 (익명 보장)
- 유저 콘텐츠 **리액션**

### 📜 Page Graph

<div align="center">
  <img src="https://github.com/user-attachments/assets/50267b06-a5ec-4c48-af32-18e12f2e8ce4" alt="Page Graph" style="max-width: 100%; height: auto;">
</div>

## 😋 팀원 소개

<div align="center">
  <img src="https://github.com/user-attachments/assets/39bb8df2-b234-45b2-ba97-2b08100a2dc1" alt="팀원 소개" style="max-width: 100%; height: auto;">
</div>

## ⚙️ 나의 역할

저는 이 프로젝트에서 **클라우드 네이티브**를 기반으로 하여, 크게 **2가지 핵심 요소**를 고려한 인프라를 구축했습니다:

### 🎯 인프라 설계 목표

#### 1. 현대 시대 대응
- **대규모성**: 증가하는 트래픽에 대응할 수 있는 확장 가능한 아키텍처
  - MSA 아키텍처 적용으로 서비스별 독립적 확장
  - Docker와 Kubernetes를 활용한 컨테이너 오케스트레이션

- **효율성**: 빠른 개발 사이클과 신속한 서비스 배포
  - DevOps 문화 도입으로 개발과 운영의 통합
  - GitHub Actions, Terraform, Prometheus, Grafana 기술 스택 활용

#### 2. 인프라 핵심 특성
- **고가용성 (High Availability)**: 서비스 중단 최소화
- **보안성 (Security)**: 데이터와 시스템 보호
- **성능 (Performance)**: 최적화된 응답 시간과 처리량

---

## 🏗️ 현대적 인프라 아키텍처

### 📊 전체 아키텍처 개요

<div align="center">
  <img src="https://github.com/user-attachments/assets/104e6efe-d6d9-4f70-8f21-57acc9bb4390" alt="현대적 인프라 개요" style="max-width: 100%; height: auto;">
</div>

### 🔄 1. MSA 아키텍처 및 CI/CD Pipeline

<div align="center">
  <img src="https://github.com/user-attachments/assets/d25c4814-118b-47e8-a9dd-b5d610c1d650" alt="MSA 및 CI/CD" style="max-width: 100%; height: auto;">
</div>

#### 🏛️ MSA 아키텍처 구성
- **라우팅 전략**
  - 도메인 기반: 개발환경(dev.todaktodak.site) / 운영환경(todaktodak.site)
  - 경로 기반: Frontend(/), Backend(/api), AI 서비스 분리

- **서비스 분할**
  - Frontend: React 기반 사용자 인터페이스
  - Backend: Spring Boot API 서버
  - AI Services: 코멘트 생성, 웹툰 생성, BGM 생성

#### 🔄 CI/CD Pipeline
GitHub Actions를 활용한 **완전 자동화된 배포 파이프라인** 구축:

**1. 협업 강화**
- GitHub 작업 내용을 **Discord로 실시간 전달**
- 팀원 간 투명한 작업 현황 공유

**2. 업무 효율화**
- **GitHub Issue**와 **Jira 티켓** 연동
- 통합된 이슈 트래킹 시스템 구축

**3. 지속적 통합 (CI)**
- Dev, Main 브랜치 Push 시 GHCR에 **도커 이미지 자동 저장**
- 코드 품질 관리 및 배포 준비 자동화

**4. 지속적 배포 (CD)**
- GitHub Action Dispatch 활용
- 각 Repository에서 이미지 생성 시 Cloud Repository로 전파
- **Helm Chart 기반 자동 배포** 수행

### 🛠️ 2. IaC(Terraform) 및 모니터링 시스템

<div align="center">
  <img src="https://github.com/user-attachments/assets/a077faf9-5f1f-4309-9202-95a56149f420" alt="IaC 및 모니터링" style="max-width: 100%; height: auto;">
</div>

#### 📝 Infrastructure as Code (IaC)
**Terraform**을 활용한 선언적 인프라 관리:

- **코드 기반 인프라 관리**
  - 모든 클라우드 리소스를 코드로 정의
  - Git을 통한 인프라 버전 관리
  - 환경별(dev/prod) 일관된 배포

- **비용 최적화**
  - 사용하지 않을 때 리소스 자동 해제
  - 리소스 사용량 추적 및 최적화

- **재현 가능성**
  - 동일한 환경을 언제든 재구축 가능
  - 장애 복구 시간 단축

#### 📊 모니터링 및 관찰 가능성
**Prometheus + Grafana** 스택을 활용한 종합 모니터링 시스템:

**실시간 메트릭 수집**
- Kubernetes 클러스터 상태 모니터링
- Pod 및 Node 리소스 사용량 추적

**시각화 및 대시보드**
- Grafana를 통한 직관적인 메트릭 시각화

**알림 시스템**
- 임계값 기반 자동 알림
- 이메일/Slack 통합 알림

---

## ⚡ 인프라 특성 구현

### 🔄 고가용성 (High Availability)

<div align="center">
  <img src="https://github.com/user-attachments/assets/b3aab2b4-739f-4e28-95f0-6c690bc984be" alt="고가용성 구현" style="max-width: 100%; height: auto;">
</div>

#### 🌍 Multi-AZ 구성
- 재해 및 장애 상황에 대한 **자동 복원력** 확보
- 각 AZ별 NAT Gateway 구성으로 단일 장애점 제거

#### 🔄 무중단 배포
- Deployment Resource의 **RollingUpdate** 전략 사용
- 서비스 중단 없는 버전 업데이트
- Health Check 기반 안전한 배포

#### 📈 자동 스케일링
- **HPA (Horizontal Pod Autoscaler)**: CPU/Memory 기준 Pod 수 자동 조정
- **Cluster Autoscaler**: 리소스 부족 시 Node 수 자동 증설
- 트래픽 증가 시 **탄력적 대응**으로 성능 유지

**스케일링 효과 검증:**
- **Before**: Pod 수 제한으로 인한 Memory Issue 발생 → 서비스 불안정
- **After**: 노드 자동 추가로 모든 Pod 정상 실행 → 안정적 서비스 제공

### 🔒 보안성 (Security)

<div align="center">
  <img src="https://github.com/user-attachments/assets/68a001b6-e5e5-40ee-97c3-37f0d71875cd" alt="보안성 구현" style="max-width: 100%; height: auto;">
</div>

#### 🛡️ 네트워크 보안
- **Private Subnet**: 모든 워커 노드를 Private 환경에 배치
- **Bastion Host**: SSH 접근을 위한 안전한 게이트웨이
- **보안 그룹**: 세밀한 포트 및 프로토콜 기반 접근 제어

#### 🔐 데이터 보안
- **AWS Secrets Manager**: 중요한 환경변수 및 DB 크리덴셜 안전 관리
- **Let's Encrypt**: SSL/TLS 인증서 자동 발급 및 갱신

#### ⚡ 성능 최적화
- **RDS Read Replica**: 읽기 전용 복제본을 활용해서, Master-Slave 구조로 쓰기-읽기를 분리하여 DB 부하 분산
- **CloudFront CDN**: S3 기반 글로벌 컨텐츠 캐싱
- **S3 Presigned URL**: 서버 부하 감소를 위한 직접 다운로드

---

## 🔧 기술 스택

### ☁️ Cloud Platform
| 서비스 | 용도 | 특징 |
|--------|------|------|
| **AWS EKS** | Kubernetes 관리 | 완전 관리형 컨테이너 오케스트레이션 |
| **AWS RDS** | PostgreSQL DB | Multi-AZ, Read Replica 지원 |
| **AWS S3** | 객체 스토리지 | 99.999999999% 내구성 |
| **CloudFront** | CDN | 글로벌 엣지 캐싱 |
| **Route53** | DNS 관리 | 고가용성 DNS 서비스 |
| **Secrets Manager** | 보안 관리 | 자동 크리덴셜 로테이션 |

### 🐳 Container & Orchestration
- **Kubernetes**: 컨테이너 오케스트레이션
- **Docker**: 컨테이너화
- **Helm Charts**: Kubernetes 패키지 관리

### 🔄 CI/CD & IaC
- **GitHub Actions**: CI/CD 파이프라인
- **Terraform**: Infrastructure as Code
- **GHCR**: 컨테이너 레지스트리

### 📊 Monitoring & Observability
- **Prometheus**: 메트릭 수집 및 저장
- **Grafana**: 시각화 및 대시보드

### 💾 Database & Storage
- **PostgreSQL RDS**: 
  - Multi-AZ 배포로 고가용성 확보
  - Read Replica로 읽기 성능 향상
- **ElastiCache Redis**: 세션 관리 및 캐싱
- **S3 Object Storage**: 사용자 업로드 파일 및 AI 생성 컨텐츠

---

## 🚨 주요 이슈 및 해결 과정

### 1. 🔍 EKS Load Balancer 접근 불규칙 문제

#### 문제 상황
로드밸런서를 통한 서비스 접근이 **간헐적으로 실패**하는 현상 발생

#### 해결 과정

**1차 시도: CNI 네트워크 문제로 가정**
- AWS VPC CNI 설정 및 OIDC 자격 증명 설정
- IAM 정책 연결 시도
- **결과**: 문제 지속 → 다른 원인 탐색 필요

**2차 시도: 체계적 디버깅 접근**
- Bastion Host 구축하여 실제 노드에 직접 접근
- curl 명령어로 단계별 연결성 테스트
- **발견**: 노드 간 통신 및 외부 인터넷 접근 문제

**최종 해결**
- 노드 그룹 OutBound 보안 그룹 설정: 외부 인터넷 접근 허용
- 노드 간 InBound 보안 그룹 설정: 클러스터 내부 통신 허용

#### 핵심 교훈
> **"확실하다고 생각하는 것도 의심하라"**
> 
> Terraform 코드가 오류 없이 실행되었다고 해서 모든 설정이 정상적으로 적용되었다고 가정하면 안 된다. 항상 **공식 문서 참조**와 **단계별 검증**이 필요하다.

### 2. 🗄️ PostgreSQL RDS 접근 타임아웃 이슈

#### 문제 상황
- 퍼블릭 액세스 허용 설정 ✅
- 보안 그룹 5432 포트 허용 ✅  
- 하지만 외부에서 DB 연결 시 **타임아웃 발생** ❌

#### 원인 분석
RDS의 **서브넷 그룹** 개념 이해 부족:
- 기본 서브넷 그룹은 VPC의 **모든 서브넷** 포함
- RDS가 Private Subnet에 생성되면 퍼블릭 접근 모드여도 접근 불가

#### 해결 방법
**커스텀 서브넷 그룹** 생성:
- 퍼블릭 접근이 필요한 경우: Public Subnet만 포함
- 내부 접근만 필요한 경우: Private Subnet만 포함

---

## 🚀 개선사항

### 🔒 보안 강화
**목표**: EKS API Server Private 전환
- Jenkins CI/CD 서버를 VPC 내부 구축
- GitHub Actions 대신 Private Jenkins 활용

### 📊 모니터링 고도화
**목표**: 엔터프라이즈급 관찰 가능성 구현
- 복잡한 메트릭 기반 경고 시스템 구축
- **로그 중앙화** (ELK Stack) 구현

### 🛠️ IaC 완전성
**목표**: 100% 코드 기반 인프라 관리
- AWS Secrets Manager 종속성 문제 해결
- RDS, ElastiCache Terraform 완전 통합

### 🔄 DevOps 문화 확산
- **테스트 자동화** 강화
- **카나리 배포** 및 **블루-그린 배포** 전략 적용

---

## 💭 프로젝트 회고

이 프로젝트를 통해 **현대적인 클라우드 네이티브 기술 스택**을 활용한 확장 가능하고 안정적인 인프라를 구축할 수 있었습니다. 단순히 기술 스택을 사용하는 것을 넘어서, **왜 이 기술이 필요한지, 어떤 문제를 해결하는지**에 대한 깊은 이해를 얻었습니다. 특히 실제 운영 환경에서 발생할 수 있는 다양한 이슈들을 직접 경험하고 해결하면서, **문제 해결 능력과 시스템 사고력**을 크게 향상시킬 수 있었습니다.

---
