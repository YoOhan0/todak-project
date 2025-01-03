## → 🌝 프로젝트 개요

  현재 시대의 SNS에서 **물질적 과시**가 만연한 상황과 이로 인해 발생하는 **다양한 문제점들**(낮은 자존감 및 끊임없는 자기비교)을  주목했습니다.

  <b>‘우리의 행복 우리가 가진 것이 아니라, 우리의 존재 그 자체에서 나온다’</b>는 컨셉을 모티브 삼아서 **자신의 내면**과 **창의성**을 표현하도록 장려하며 건강한 SNS 분위기를 조성하는 목적으로 해당 프로젝트를 기획하게 되었습니다.

  해당 앱의 **대표적인 기능**은 다음과 같습니다.

1. 프로필을 설정하면, 개인 맞춤 **아바타** 생성. (아바타는 웹툰 생성에 활용)
2. 일기 작성 그에 대한 **AI 위로 코멘트**
3. 일기 기반 **웹툰 및 음악** 생성 (음악 장르 선택 가능)
4. 일기 **공유** 서비스 (익명 보장)
5. 유저 콘텐츠 **리액션**

<div align="center">
 <img src="https://github.com/user-attachments/assets/df98cbc1-3338-4f58-a7a4-33d5f06e18de" width="50%" height="50%" />
</div>

## → 📜 Page Graph
<div align="center">
 <img src="https://github.com/user-attachments/assets/50267b06-a5ec-4c48-af32-18e12f2e8ce4" width="70%" height="50%" />
</div>


## → 😎 나의 역할

 **클라우드 네이티브**를 기반으로 한, 프로젝트의 인프라를 담당하였습니다.


### <Cloud Stack & Main Feature>

![19조 Todak 클라우드 설계.jpg](https://github.com/user-attachments/assets/8e8047dd-a083-42f8-b207-886344d227cb)

- **Infra As a Code by Terraform** **(IaC)**
    - 테라폼을 활용하여 클라우드 리소스를 띄움으로써 리소스 관리를 효율적으로 하고자 하였고, 사용 지 않을 때는 리소스를 내림으로써 비용 최적화를 추구하였습니다.
        
        ![스크린샷 2024-12-26 오후 11.30.14.png](https://github.com/user-attachments/assets/78bcf0a3-841d-45ae-b683-e40937249a0b)
        
- **Various Use of Github Action (CI/CD)**
    - Github Action을 최대한 활용함으로써, DevOps 과정에서의 **효율화**와 **협업 간편화**를 추구하였습니다.
    - 프로젝트 형상 관리 도구로 **Github**을 사용하였고, **반복해서 사용**하는 Github Action 코드들을 **.github Repo에 모아 재활용** 할 수 있었기 때문에 편리하다고 생각하여 CI/CD 도구로 Github Action을 선택하게 되었습니다.
        
        ![스크린샷 2024-12-27 오전 2.40.52.png](https://github.com/user-attachments/assets/e8588a67-4823-4477-bf5e-384d80c9945a)
        
    - **활용 방식**
        1. Github 작업 내용 **Discord**로 전달 (협업 강화)
            
            <div align="center">
               <img src="https://github.com/user-attachments/assets/f1f3e91e-a6a9-4f96-8bb8-de1d7c1e93dd" width="50%" height="50%" />
            </div>

        2. **GitHub Issue**와 **Jira 티켓** 연동 (업무 효율화)
            
            ![githubIssue_jiraTicket.jpg.png](https://github.com/user-attachments/assets/71e4a893-d58e-4d3a-b1ee-d8600b2a0706)
            
        3. Dev,Main 브랜치에 Push 시 GHCR에 **도커 이미지 저장** (CI)
            
            ![ghcr.png](https://github.com/user-attachments/assets/6dc5007d-7511-463b-bc0b-62ae39f72d69)
            
        4. Github Action Dispatch 활용하여, 이미지 각 Repo에서 생성 시 Cloud Repo로 전파하여, **Helm Chart 기반 배포** 수행 (CD)
            
            ![cd.png](https://github.com/user-attachments/assets/02cd16e3-4ac6-430d-9461-d527352b14fd)
            

- **AWS EKS + Cloud platform**
    - Container 기술인 **Kubernetes**와 **AWS 클라우드 서비스**를 활용함으로써 **고가용성**, **보안성, 성능, 내구성**을 갖춘 인프라를 구축하고자 하였습니다.
        - **High Availability**
            - **다중 AZ** 인프라 구조 적용.
            - Deployment Resource의 **RollingUpdate** 전략을 사용하여, 버전 업데이트 관련 **무중단 배포 적용.**
            - HPA와 Cluster Autoscaler Resource를 활용하여, 트래픽 증가시 **Pod, Node Scaling 적용.**
                - HPA (Pod Scheduling)
                    - Deployment Resource에 Horizontal Pod AutoScaler (HPA)를 적용하여 특정 리소스 기준을 넘었을 시 자동으로 Pod의 수가 늘어나도록 설정하였습니다.
                        
                        ![hpa정리본.jpg.png](https://github.com/user-attachments/assets/af4fbf65-a3ad-49a9-a036-04ab06cfe4fb)
                        
                - Cluster-AutoScaler (Node Scheduling)
                    - Kubernetes와 AWS IAM을 통합하여 Cluster Autoscaler Pod가 AWS 리소스(ASG)에 액세스 할 권한을 부여하게끔 IAM 정책과 Service Account를 생성하고 이를 기반으로 Cluster AutoScaler를 실행하여 Node 스케줄링이 되도록 하였습니다.
                    - before
                        - HPA에 의해 Deployment Object의 최대 Pod수(8)에 도달 했을 때, 몇몇 Pod에서 Memory Issue가 발생해 정상적으로 실행되지 못했습니다.
                        
                        ![ClusterAutoscaler_before정리본.jpg.png](https://github.com/user-attachments/assets/356278f3-6b00-4a7e-a376-7105800158ba)
                        
                    - after
                        - HPA에 의해 Deployment Object의 최대 Pod수(8)에 도달 하더라도, 적절하게 노드가 추가되어 모든 Pod가 정상적으로 실행 되는 것을 확인 할 수 있었습니다.
                        
                        ![ClusterAutoscaler_after정리본.jpg.png](https://github.com/user-attachments/assets/31bedd3e-c824-4625-8557-4283371f35f9)
                        
        
        - **Security**
            - S3 저장소에 Presigned URL을 적용하여 일정 시간만 컨텐츠에 접근 할 수 있게 함으로써 불필요한 접근 및 DDOS 방지.
            - AWS Secret Manager를 활용하여, 쿠버네티스에서 활용하는 중요한 환경변수들에 대한 안전한 관리 적용.
                
                ![aws_secret_manager정리본.jpg.png](https://github.com/user-attachments/assets/24c14e1c-70ae-48d0-a611-0197246f89bd)
                
            - Let’s Encrypt CA 기반의 SSL/TLS 인증서 발급 및 적용의 자동화.
        - **Performance**
            - RDS Read Replica 기능 활용하여 비동기적으로 읽기 전용 복제본을 생성함으로써, 기본 **인스턴스의 부하를 줄이고** 동시에 **데이터 복원 옵션**으로 활용.
            - 99.999999999의 내구성을 보장하는 S3 저장소를 사용하고 이를 Origin으로 하는 CloudFront 기능을 활용하여 컨텐츠를 캐싱함으로써 **비용 및 성능 최적화**를 추구.


<br></br>

## 추가 포트폴리오 내용 링크 : 
https://celestial-snapdragon-a9f.notion.site/SNS-165deab51b4b80098c7aeeae544331ac
