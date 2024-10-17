![image](https://github.com/user-attachments/assets/fe889a71-ed74-45e1-8a71-f616f8128411)# 🎟️ 멀티클라우드 기반 티켓팅 웹 서비스

이 프로젝트는 **멀티클라우드 환경**에서 티켓팅 웹 서비스를 제공하기 위해 설계되었습니다. 고가용성과 확장성을 염두에 둔 서비스 아키텍처로, 다양한 클라우드 인프라를 활용하여 안정적이고 빠른 티켓팅 경험을 제공합니다.

---

## 🚀 프로젝트 역할

| 팀원        | 역할                                                                                             |
|-------------|--------------------------------------------------------------------------------------------------|
| **이태민**  | AWS 인프라 설계 및 구축, 자동화, 문제 해결 및 모니터링. 고가용성 및 확장성 구현. RDS 구성, Route53 설정. |
| **강석진**  | NHN 아키텍처 설계 및 구축. Docker & Kubernetes를 활용한 Web 및 WAS 서버 구축. NHN RDS, Object Storage 구축 및 연동. VPN 서버 구축. RDS 간 데이터 동기화 관리. |
| **김영권**  | AWS 아키텍처 구성 및 구축. AWS WAF(웹 방화벽) 구축. NHN 클라우드 ACL 관리. 로그인 페이지 구현. |
| **양현수**  | 아키텍처 구축. Docker & Kubernetes 활용 Web 배포. NKS 오토스케일링 설정. CI/CD(Jenkins) 파이프라인 구축. 모니터링(Prometheus, Grafana) 관리. |
| **주상민**  | 클라우드 아키텍처 구성 및 구축. 웹 페이지 구현. 데이터베이스 구축. 발표 자료(PPT) 제작. |



## 🛠️ 기술환경

| 기술 스택          | 설명                                      |
|-------------------|-----------------------------------------|
| **CLOUD**     |   AWS,NHN, Kubernates, docker                   |
| **CI/CD**         | Github, Jenkins, NCR         |
| **Monitoring**   | Grafana , Prometheous                        |
| **Web/DB** | Php, RDS , Mysql , Apache |
| **Security** | WAF , DVWA |
| **Network**   | Route53, Strongswan, Aws site to site VPN  |

---

## 🌐 전체 토폴로지

![image](https://github.com/user-attachments/assets/b1b286fe-f048-4920-9a55-8b91e97e4dc4)


### 구성 요소 설명:

- **NHN Cloud**: 
  - 공용 서브넷(Public subnet)과 사설 서브넷(Private subnet)으로 나뉘어 있으며, 각각 웹과 WAS 클러스터를 운영.
  - NKS 클러스터를 통해 자동화된 컨테이너 관리 및 확장 기능 제공.
  - VPN 게이트웨이를 통해 AWS 클라우드와 안전한 통신을 유지.

- **AWS Cloud**:
  - 웹 서버와 데이터베이스가 분리된 퍼블릭 서브넷과 프라이빗 서브넷으로 구성.
  - 자동 확장 그룹을 통해 사용량에 따라 인프라를 유연하게 확장.

- **VPN Gateway**: NHN Cloud와 AWS 간의 안전한 통신을 위한 VPN 설정.

---

## 📊 CI/CD 파이프라인.

CI/CD 파이프라인은 코드 품질 관리 및 자동화를 위해 설정되었습니다.

1. **GitHub Actions**: 코드 푸시 시 자동으로 테스트 및 빌드를 실행.
2. **Jenkins**: 안정적인 빌드 이후 AWS 및 NHN Cloud로의 배포를 자동화.
3. **Docker & Kubernetes**: 모든 서비스는 컨테이너화되어, 오케스트레이션 및 확장 관리를 지원.

---
## 💡 기능 특징

- **실시간 티켓팅**: PHP 기반의 실시간 티켓팅 기능 제공
- **자동 확장**: 클라우드 환경에서의 트래픽 급증에 대비한 자동 확장 기능
- **멀티클라우드 백업**: AWS와 NHN의 데이터 백업 및 동기화 관리
- **모니터링 및 로그 관리**: Prometheus, Grafana를 이용한 실시간 모니터링

---

## 📈 부하일경우 NHN 모니터링 
![image](https://github.com/user-attachments/assets/ff43bc06-1347-4c0b-889d-385cf8c3f44e)


---
# 05. NHN - VPN


![image](https://github.com/user-attachments/assets/e62168d7-81f9-4aa7-9677-46c4e432db91)
 **NHN Cloud**와 **AWS** 간의 **VPN 연결**을 통해 네트워크 보안을 강화하였습니다. NHN Cloud의 관리 서버에 **strongSwan**을 설치하여 VPN 서버를 설정하고, AWS와의 VPN 연결을 성공적으로 완료했습니다.

---

## 📡 VPN 설정 과정

1. **Management 서버에 strongSwan 설치**: NHN Cloud 내의 관리 서버에 strongSwan을 설치하여 VPN 연결을 위한 환경을 구성했습니다.
2. **VPN 서버 설정**: strongSwan을 활용해 VPN 서버를 설정하고 필요한 보안 규칙을 적용했습니다.
3. **AWS와의 VPN 연동**: NHN Cloud와 AWS 간의 VPN 게이트웨이를 설정하여 안전한 통신 경로를 구축했습니다.

---



### 핵심 구성 요소:

- **NHN Cloud**: NHN Cloud 내에서 웹 및 WAS 서비스가 구동되고, 외부 네트워크와 연결된 VPN 게이트웨이를 통해 AWS와 통신합니다.
- **AWS**: AWS 클라우드 내에서 웹 서버 및 데이터베이스를 운영하고 있으며, VPN을 통해 NHN Cloud와 연결됩니다.
- **strongSwan**: NHN Cloud의 관리 서버에 설치된 VPN 소프트웨어로, VPN 설정 및 관리를 담당합니다.

---


