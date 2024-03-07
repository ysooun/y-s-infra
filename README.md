### y-s-infra의 전체 구성도
--- 
<img width="705" alt="스크린샷 2024-03-08 오전 2 37 01" src="https://github.com/ysooun/y-s-infra/assets/154872496/4ab5bc90-ee6b-4aec-9dfe-7db495c55d61">

1. infra 내부에 ingress와 external-dns는 yaml 파일로 구성했습니다.
2. prometheus, aws-ebs-csi-driver, aws-load-balancer-controller, jenkins, argo cd는 helm차트를 이용해 구성했습니다.

<br>

### prometheus 구성도
---
<img width="721" alt="스크린샷 2024-03-08 오전 1 24 42" src="https://github.com/ysooun/y-s-infra/assets/154872496/54adb8ca-8211-46d3-8833-59833855688a">

1. prometheus server: 메트릭을 수집하고 저장합니다. prometheus.yml 설정 파일에 정의된 내용으로 메트릭을 수집합니다.
2. alertmanager: prometheus server가 생성한 알림을 처리하고 이를 적절한 수신자에게 전달하는 역할을 합니다. slience 기능을 통해 특정 알림을 무음처리 할 수 있습니다.
3. serverFiles: prometheus 설정이 포함된 파일입니다. prometheus.yml, alerting_rules.yml 등의 다양한 설정들을 할 수 있습니다.
   prometheus.yml 파일을 살펴보면 pods의 metric, nodes의 metric, ingress를 통해 들어오는 metric 등을 확인 할 수 있습니다.
   alerting_rules을 통해서는 HighRequestLatency를 설정하여 요청이 지연되면 경고를 보내도록 설정했습니다.
4. 경고는 슬랙의 webhook을 통해 자동 크리거 되게 설정했습니다.
5. prometheus의 ui는 생각보다 많이 투박했습니다. 시각화에 특화 되어있는 grafana를 사용하여 prometheus와 연동해 사용했습니다.
