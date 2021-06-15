# P.CL Kubernetes Service
<script id="asciicast-420287" src="https://asciinema.org/a/420287.js" async></script>
[![asciicast](https://asciinema.org/a/420287.svg)](https://asciinema.org/a/420287)

## 소개
P.CL Kubernetes 서비스는 SKT 사내에 구축된 Private Cloud 개발 환경 서비스인 P.CL에서 제공하는 관리형 Kubernetes 서비스입니다. CSP(Cloud Service Provider)의 EKS, AKS 서비스와 같은 관리형 Kubernetes 서비스로 쉽게 Kubernetes 클러스터를 생성해서 개발 환경으로 사용할 수 있는 서비스입니다. P.CL Kubernetes 서비스는 표준 Kubernetes 클러스터를 제공하고 있으며 P.CL Kubernetes 클러스터에서 개발한 어플리케이션은 코드를 수정하지 않고 EKS, AKS 등의 CSP에서 제공하는 Kubernetes에 배포할 수 있습니다.

## Kubernetes 클러스터 생성
[클러스터 생성 가이드](./docs/creating_cluster.md)를 참고하세요.

## Kubernetes 클러스터 접근
생성된 Kubernetes 클러스터에 접근하기 위해서는 kubeconfig 파일이 필요합니다.
kubeconfig 파일은 **P.CL 포털 -> My Resource -> 프로젝트 선택 -> 가상 서버 목록 상단**의 kubeconfig download select box를 이용해서 다운받을 수 있습니다. [kubeconfig 파일 사용 방법](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)

Kubernetes 클러스터를 사용하기 위해서는 kubectl cli, lens gui 등의 client가 필요합니다.

* [kubectl](https://kubernetes.io/docs/tasks/tools/) : *생성된 클러스터의 버전과 같은 버전의 kubectl을 사용하세요.*
* [lens](https://k8slens.dev/) : *lens는 P.CL 포털을 통해서도 다운로드가 가능합니다.*

자세한 내용은 [클러스터 접근 가이드](./docs/accessing_cluster.md)를 참고하세요.

### OA망 접속용 클러스터
P.CL 포털에서 Kubernetes 클러스터를 생성 시 **OA망 접속용** 클러스터를 생성할 수 있습니다.
이렇게 생성된 Kubernetes 클러스터는 OA망에 연결되어 있는 AD Join된 Local PC ( Mac or Windows ) 에서 직접 접근할 수 있습니다.

### MyDesk 접속용 클러스터
P.CL 포털에서 Kubernetes 클러스터를 생성 시 **MyDesk 접속용** 클러스터를 생성할 수 있습니다.
해당 Kubernetes 클러스터는 MyDesk VDI (Windows)내에서 직접 접근할 수 있으며, kubernetes control plane에 ssh로 접속해서 Linux 환경에서 접근할 수 도 있습니다.

## 어플리케이션 배포 예제
첨부된 echo app 및 nginx app 배포 예제([P.CL Kubernetes Sample Applications](./docs/sample_apps.md))를 참고해서 Kubernetes Cluster에 App을 배포해 보세요.

## P.CL Kubernetes Service 특징
* 쉽고 빠른 서비스

클릭 몇번만으로 10분 내에 관리형 Kubernetes 클러스터를 제공받을 수 있습니다. 또한 같이 제공하는 Kubernetes GUI 인 Lens를 통해서 직관적으로 Kubernetes 클러스터를 관리하고 모니터링 할 수 있습니다.
* 편리한 접근성

  * OA망 접속용 : 사내 OA망에 붙은 Local PC에서 직접 클러스터를 제어하고 어플리케이션을 배포/관리할 수 있습니다. 생성된 클러스터는 internet outbound 접근이 가능합니다.
  * Mydesk 접속용 : 재택 근무나 외부 업체와의 협업 시에 MyDesk를 통해서 클러스터를 제어하고 어플리케이션을 배포/관리할 수 있습니다. 생성된 클러스터는 생성 직후 3일간 internet outbound 접근이 가능하고 이후에는 보안팀에 신청을 통해서 기간을 연장할 수 있습니다. 사내 서비스 연동이 가능하기 때문에 사내 서비스 연동 개발 시에 유용합니다.
* Self healing

P.CL Kubernetes 서비스를 관리형 서비스입니다. 클러스터를 이루는 worker node의 생명주기는 P.CL Kubernetes 서비스에 의해  자동으로 관리됩니다. 또한 Scale In/Out 기능으로 손쉽게 node 자원의 개수를 조절할 수 있습니다.  
* 완전하게 격리된 네트워크 환경 제공

P.CL Kubernetes 서비스를 통해 Kubernetes 클러스터를 생성하면 Virtual Private Network에 클러스터가 생성됩니다. 클러스터의 접근 경로는 controller node의 external ip로 한정되기 때문에 완전히 격리된 네트워크 안에 서비스를 구성할 수 있습니다. 
* 유연한 Persistent Volume 사용

P.CL Kubernetes 서비스를 클러스터 생성과 동시에 pcl이라는 이름의 Storage Class를 제공합니다. 이를 통해 동적으로 Persistent Volume을 생성해서 안전하게 데이터를 보관할 수 있습니다.
사용 방법은 ([P.CL Kubernetes Sample Applications](./docs/sample_apps.md)) 중 nginx with pvc 배포 예제 항목을 참고하십시오.
* 다양한 컴포넌트 제공

P.CL Kubernetes 서비스는 클러스터 생성과 동시에 다양한 컴포넌트를을 제공하고 있습니다. nginx ingress를 통해 어플리케이션을 외부로 바로 오픈할 수 있고, prometheus를 통해 클러스터의 모니터링 정보를 바로 확인할 수 있습니다. 뿐만 아니라 calico cni(container network interface), cinder csi(container storage interface) 등이 함께 제공되기 때문에 클러스터 생성 즉시 어플리케이션을 배포할 수 있습니다. 
* 직관적인 모니터링

P.CL Kubernetes 서비스는 클러스터 생성 시 prometheus와 export가 설치되어 제공됩니다. 생성 후 Lens GUI를 통해서 직관적인 모니터링 정보를 확인할 수 있습니다. Lens 연동 방법은 [클러스터 접근 가이드](./docs/accessing_cluster.md)를 참고하세요.

## Documentation
`/docs` 아래에서 더 많은 문서를 보실 수 있습니다.

## Contacts

문의사항이 있으면 아래로 연락주십시오.
* 김대성 ( daeseong.kim@sk.com )
* 반지훈 ( jihun.ban@sk.com )
* 하성윤 ( sy.ha@sk.com )
