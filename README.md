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
 <img src="https://github.com/user-attachments/assets/df98cbc1-3338-4f58-a7a4-33d5f06e18de" width="40%" height="40%" />
</div>

## → 😋 팀원 소개

<div align="center">
 <img src="https://github.com/user-attachments/assets/39bb8df2-b234-45b2-ba97-2b08100a2dc1" width="70%" height="50%" />
</div>


## → 📜 Page Graph
<div align="center">
 <img src="https://github.com/user-attachments/assets/50267b06-a5ec-4c48-af32-18e12f2e8ce4" width="70%" height="50%" />
</div>


## → 😎 나의 역할

 **클라우드 네이티브**를 기반으로 한, 프로젝트의 인프라를 담당하였습니다.


### <Cloud Stack & Main Feature>

<div align="center">
 <img src="https://github.com/user-attachments/assets/8e8047dd-a083-42f8-b207-886344d227cb" width="70%" height="50%" />
</div>

- **Infra As a Code by Terraform** **(IaC)**
    - **테라폼**을 활용하여 클라우드 리소스를 띄움으로써 리소스 관리를 코드로써 효율적으로 하고자 하였고, 사용 지 않을 때는 리소스를 내림으로써 비용 최적화를 추구하였습니다.
        
        <div align="center">
           <img src="https://github.com/user-attachments/assets/78bcf0a3-841d-45ae-b683-e40937249a0b" width="30%" height="30%" />
        </div>
        
- **Various Use of Github Action (CI/CD)**
    - Github Action을 최대한 활용함으로써, DevOps 과정에서의 **효율화**와 **협업 간편화**를 추구하였습니다.
    - 프로젝트 형상 관리 도구로 **Github**을 사용하였고, **반복해서 사용**하는 Github Action 코드들을 **.github Repo에 모아 재활용** 할 수 있었기 때문에 편리하다고 생각하여 CI/CD 도구로 Github Action을 선택하게 되었습니다.
        
        ![스크린샷 2024-12-27 오전 2.40.52.png](https://github.com/user-attachments/assets/e8588a67-4823-4477-bf5e-384d80c9945a)
        
    - **활용 방식**
        1. Github 작업 내용 **Discord**로 전달 (협업 강화)
            
            <div align="center">
               <img src="https://github.com/user-attachments/assets/f1f3e91e-a6a9-4f96-8bb8-de1d7c1e93dd" width="40%" height="40%" />
            </div>

        2. **GitHub Issue**와 **Jira 티켓** 연동 (업무 효율화)
            
             <div align="center">
                 <img src="https://github.com/user-attachments/assets/71e4a893-d58e-4d3a-b1ee-d8600b2a0706" width="80%" height="80%" />
              </div>
            
        3. Dev,Main 브랜치에 Push 시 GHCR에 **도커 이미지 저장** (CI)
            
           <div align="center">
             <img src="https://github.com/user-attachments/assets/6dc5007d-7511-463b-bc0b-62ae39f72d69" width="70%" height="70%" />
           </div>
            
        5. Github Action Dispatch 활용하여, 이미지 각 Repo에서 생성 시 Cloud Repo로 전파하여, **Helm Chart 기반 배포** 수행 (CD)
            
            <div align="center">
               <img src="https://github.com/user-attachments/assets/02cd16e3-4ac6-430d-9461-d527352b14fd" width="70%" height="50%" />
            </div>


- **AWS EKS + Cloud platform**
    - Container 기술인 **Kubernetes**와 **AWS 클라우드 서비스**를 활용함으로써 **고가용성**, **보안성, 성능, 내구성**을 갖춘 인프라를 구축하고자 하였습니다.
        - **High Availability**
            - **다중 AZ** 인프라 구조 적용.
            - Deployment Resource의 **RollingUpdate** 전략을 사용하여, 버전 업데이트 관련 **무중단 배포 적용.**
            - HPA와 Cluster Autoscaler Resource를 활용하여, 트래픽 증가시 **Pod, Node Scaling 적용.**
                - HPA (Pod Scheduling)
                    - Deployment Resource에 **Horizontal Pod AutoScaler (HPA)를 적용**하여 특정 리소스 기준을 넘었을 시 **자동으로 Pod의 수가 늘어나도록** 설정하였습니다.
                        
                        <div align="center">
                           <img src="https://github.com/user-attachments/assets/af4fbf65-a3ad-49a9-a036-04ab06cfe4fb" width="80%" height="80%" />
                        </div>
                        
                - Cluster-AutoScaler (Node Scheduling)
                    - **Kubernetes와 AWS IAM을 통합**하여 Cluster Autoscaler Pod가 **AWS 리소스(ASG)에 액세스 할 권한을 부여**하게끔 IAM 정책과 Service Account를 생성하고 이를 기반으로 **Cluster AutoScaler**를 실행하여 Node 스케줄링이 되도록 하였습니다.
                    - before
                        - HPA에 의해 Deployment Object의 최대 Pod수(8)에 도달 했을 때, 몇몇 Pod에서 Memory Issue가 발생해 **정상적으로 실행되지 못했습니다**.
                        
                        <div align="center">
                           <img src="https://github.com/user-attachments/assets/356278f3-6b00-4a7e-a376-7105800158ba" width="80%" height="80%" />
                        </div>
                        
                    - after
                        - HPA에 의해 Deployment Object의 최대 Pod수(8)에 도달 하더라도, 적절하게 노드가 추가되어 모든 Pod가 **정상적으로 실행 되는 것을 확인** 할 수 있었습니다.
                      
                        <div align="center">
                           <img src="https://github.com/user-attachments/assets/31bedd3e-c824-4625-8557-4283371f35f9" width="80%" height="80%" />
                        </div>
        
        - **Security**
            - S3 저장소에 Presigned URL을 적용하여 일정 시간만 컨텐츠에 접근 할 수 있게 함으로써 **불필요한 접근 및 DDOS 방지**.
            - AWS Secret Manager를 활용하여, 쿠버네티스에서 활용하는 **중요한 환경변수들에 대한 안전한 관리** 적용.
              
                <div align="center">
                   <img src="https://github.com/user-attachments/assets/24c14e1c-70ae-48d0-a611-0197246f89bd" width="70%" height="70%" />
                </div>

                
            - Let’s Encrypt CA 기반의 **SSL/TLS 인증서 발급 및 적용**의 자동화.
        - **Performance**
            - RDS Read Replica 기능 활용하여 비동기적으로 읽기 전용 복제본을 생성함으로써, 기본 **인스턴스의 부하를 줄이고** 동시에 **데이터 복원 옵션**으로 활용.
            - 99.999999999의 내구성을 보장하는 S3 저장소를 사용하고 이를 Origin으로 하는 CloudFront 기능을 활용하여 컨텐츠를 캐싱함으로써 **비용 및 성능 최적화**를 추구.

<br></br>
---

### <Cloud **Architecture>**

<div align="center">
 <img src="https://github.com/user-attachments/assets/aeb1666c-8a9b-438b-ac2c-ffb03183c8c5" width="70%" height="50%" />
</div>


- 해당 프로젝트에서 사용한 클라우드 아키텍쳐 구조입니다.
    - Container Orchestration 도구인 **쿠버네티스**를 활용한 AWS EKS 서비스 기반의 클라우드 아키텍쳐를 구성하였습니다.
        - **다중 AZ**와 **NAT 게이트웨이를 각 AZ 마다 구성**하여 재해 및 문제 상황에서 **가용성**을 보장하고자 하였습니다.
        - <b>Auto Scaling Group(ASG)</b>으로 인스턴스를 관리하여, **늘어나는 트래픽에 대응** 될 수 있도록 하였습니다.
        - **노드 그룹**을 **Private subnet**에 배치 시키고, 같은 VPC에 있는 **Bastion Host**에서의 SSH 22번 InBound 포트만 허용함으로써, 접근에 대한 **보안성**을 높이고자 하였습니다.

<br></br>
---

### <Kubernetes **Architecture & Feature>**

<div align="center">
 <img src="https://github.com/user-attachments/assets/729d52ef-4ca2-48b0-a102-6ceea8103381" width="70%" height="50%" />
</div>

- **AWS Route53 서비스를 활용한 도메인 관리**
    - 가비아에서 도메인을 구입하여 AWS Route 53에서 관리하는 방식으로 dev 서비스, prod 서비스, 데이터베이스, 캐시 서버에 대해 각각 **고정 도메인을 부여**하여 Terraform을 통해 리소스를 내렸다올렸을 때의 공용 IP 변경에 대해 적은 변경만으로 앱을 운영할 수 있도록 하였습니다.

        <div align="center">
           <img src="https://github.com/user-attachments/assets/48039dc8-4142-4685-be74-b35fa1ca0ac1" width="70%" height="50%" />
        </div>
        
- **Nginx Controller 기반의 라우팅**
    - 도메인 기반 라우팅
        - dev 네임스페이스와 prod 네임스페이스를 나누어 **개발환경과 운영환경을 분리**하고, 이를 위하여 todaktodak.site 또는 dev.todaktodak.site **도메인 기반의 라우팅**을 적용 하였습니다.
    - 경로 기반 라우팅
        - /api 경로와 그 외 경로에 대해서 **경로 기반 라우팅**을 적용하여, Frontend와 Backend로 가는 트래픽을 분리하였습니다.

            <div align="center">
               <img src="https://github.com/user-attachments/assets/3071b6a5-80ae-4bf9-98ba-3e5e8f949a3b" width="50%" height="50%" />
            </div>

- **모니터링 시스템 구축**
    - Prometeous+Grafana 스택을 활용하여 쿠버네티스의 Pod들의 리소스 사용량과 Node의 **리소스 사용량을 시각화** 하고, 특정 리소스 Threshold 기준에 따라 이메일 또는 메신저에 **경고**가 갈 수 있도록 하였습니다.
  
    <div align="center">
       <img src="https://github.com/user-attachments/assets/a836bb27-3802-480a-9f5f-910d07712a2c" width="70%" height="70%" />
    </div>

## → 😮 **Issues and Limitations**

- **Issues**
    - **EKS Load Balancer 접근 불규칙 문제(보안 그룹 설정 이슈)**
        - **이슈** : Terraform으로 구축한 AWS EKS에 Loadbalancer를 통하여 서비스에 접근 하려고 하니 **접근이 불규칙적**으로 됬다가 안됬다가 하는 문제 발생하였습니다.
        - **해결 과정 1** : 로드 밸런서가 인스턴스의 **노드포트**로 접근 할 때, 서비스가 있는 노드에 접근 할 경우 접근되고 아닐 경우에는 노드에 있는 **kube-proxy**가 타겟 서비스로 **트래픽을 전달하는 과정에서 문제**가 있다고 판단.
            - 그래서 파드 간의 네트워크 개념인 CNI가 문제가 있다고 판단하였고, AWS EKS에 적용된 AWS VPC CNI 설정 관련해서 구글링
            - 찾은 방법 중 그럴 듯한 방법 중 하나로 AWS VPC CNI에 역할을 기반으로 OIDC 자격 증명 공급자와 CNI 관련 IAM 정책을 연결 해주어야 CNI 관련 쿠버네티스 리소스가 CNI 작업하는데 필요한 AWS 리소스 접근 권한을 획득해 작업이 가능하다고 하여 블로그 글 참고하여 트러블 슈팅 진행.
            → but 실패.
        - **해결 과정 2** : 개발에서 다양한 계층적 테스트(단위 테스트, 모듈 테스트, 통합 테스트)를 통해 트러블 슈팅하는 것으로부터 착안하여 EKS 노드 그룹의 노드에 접근 가능한 VPC Public Subnet에 있는 **Bastion Host Instance를 구축**하여 이 호스트로 **실제 노드에 SSH로 접근**하여 다양한 테스트 진행 
            - curl 명령어를 통해서 외부 인터넷 접근 시 접근 불가 문제 발견 → 노드 그룹의 OutBound 보안그룹 설정 해서 해결
            - curl 명령어를 통해서 NodePort 서비스에 접근 시 불규칙한 접근 문제 발생 → 노드 그룹 끼리의 InBound 보안 그룹 설정을 통해서 해결
        - **정리** : 근본적인 문제는 Terraform 코드를 통해서 **보안 그룹을 설정 했지만** 보안 그룹 관련 설정하는 코드가 오류를 띄우는 것이 아니라 무시되면서 **보안 그룹이 제대로 설정 되지 않았고**, 이슈의 원인을 찾는 과정에서 보안 그룹 문제는 당연히 잘 되었을거라고 가정해서 트러블 슈팅 기간이 길어졌습니다. 그래서 이 경험을 통해  확실하다고 생각하는 것에 대해서 의심하고, 생성형AI 가 작성 해준 코드를 다듬는 것은 꼭 필요하고 **공식 문서**를 꼭 참고 하자라는 교훈을 얻게 되었습니다.
    - **Postgresql RDS 스냅샷 복원 시 타임아웃 이슈**
        - **이슈** : 적절하게 **퍼블릭 액세스 허용 설정**이랑 **보안 그룹을 설정**했음에도(인바운드 5432 허용) 외부에서 db에 연결하려니까 타임아웃 이슈 발생
        - **해결 과정** : RDS에서는 다중 AZ 모드나 네트워크 자원이 모자랄 경우를 대비하여 서브넷 그룹이라는 개념을 활용하고, **디폴트 서브넷 그룹**이 해당 vpc의 **모든 서브넷**이기 때문에 RDS 가 **프라이빗 서브넷에 생성이 된다면** 퍼블릭 접근 모드라 하더라도 접근이 안됨. 때문에 외부 접근 허용 여부에 따라 서브넷 그룹의 요소를 public할꺼면 public요소들만 private 할꺼면 private 요소들만 하는 식으로 커스텀 구성이 필요하는 것을 알게 되었습니다.
            
          <div align="center">
             <img src="https://github.com/user-attachments/assets/2aea1a5f-10d8-49a0-80c4-977efa629667" width="70%" height="70%" />
          </div>
            
- **Limitaions**
    - CI/CD 도구로 Github Action을 사용하였고, 이로 인하여 AWS EKS의 **API Server를 Public**으로 설정하였습니다. 이는 누구나 API 서버에 접근 가능하므로 보안상 좋지 못하다고 생각이 들었습니다.
        - 때문에 향후에  Private 하게 사용할 수 있는 Jenkins CI/CD 서버를 활용하고 이를 프로젝트 VPC에 띄우면, AWS EKS의 API 서버 또한 private 하게 설정하여 보안성을 높일 수 있을 것으로 생각합니다.
    - 모니터링의 경고 방식으로 **Grafana Alerting 기능**을 활용하였는데, 이는 시각화 패널을 기반으로 간단한 경고만 설정 가능합니다.
        - 대규모 마이크로서비스, 클라우드 네이티브 인프라와 같은 복잡한 메트릭 기반 경고와 고급 알림 관리를 필요로 하는 환경을 대비해 향후에 Prometeous AlertManager 도구를 활용 해볼 계획입니다.
    - **Terraform**을 통해 대부분의 리소스를 관리하였지만, AWS Secret Manager와 관련된 리소스 부분에서 **종속성 문제**(순환 참조)가 발생 하였고, RDS와 Cache(Elasticache)의 경우에는 **GUI 콘솔**을 활용하였기 때문에 리소스를 올리거나 내리는 과정에서 **수동작업**과 순차적으로 **3번 배포**하는 방식의 **차선책**을 적용하였고, 이에 대해서 **더 좋은 IaC관리 방식**을 적용 해보지 못한 부분이 아쉬웠습니다.

## → 😊 Achive

 해당 프로젝트를 통하여 **클라우드 네이티브 기반**으로 개발과 운영을 통합하는 **DevOps** 개념을 적용 해볼 수 있었습니다.

 **CI/CD 도구**를 통해 개발 내용을 **빠르게 운영에 적용**하고, **IaC 도구**를 활용해 **인프라를 코드로 관리**하고 운영에 빠르게 적용하며, **모니터링 도구**를 통해 운영에 문제가 생겼을 시 개발 및 인프라에 **바로 피드백**을 줄 수 있는 환경을 구성해 보았고 이는 현 시대에서 **Agile 개발 방식**과 **MSA 기술**이 대두되고 있는 상황에서 저의 IT 역량을 한층 업그레이드 시켜준 값진 경험 이였습니다.

 뿐만 아니라, 쿠버네티스라는 **컨테이너 인프라 기술**을 비용에 대한 걱정 없이 프로젝트에 적용 해 볼 수 있었다는 점 또한 매우 값지게 만들어준 요인이라고 생각합니다. 


<br></br>

## 포트폴리오 내용 링크 : 
https://celestial-snapdragon-a9f.notion.site/SNS-165deab51b4b80098c7aeeae544331ac
