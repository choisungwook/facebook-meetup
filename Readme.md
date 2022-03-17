# 개요
* facebook 쿠버네티스 meetup 발표에서 사용되는 예제입니다.
* 발표날짜: 22.3.19

# 실습 인프라 설치
* vagrant로 설치를 자동화 했습니다.
* 리눅스 vagrantfile과 쿠버네티스 vagrantfile 두종류가 있습니다.
  * [리눅스 vagrantfile 링크](./vagrantfiles/linux/Readme.md)
  * [쿠버네티스 vagrantfile 링크](./vagrantfiles/k8s/Readme.md)

# 예제 목차
* 네트워크 네임스페이스 예제
  * [vagrantfile 링크](./vagrantfiles/linux/Readme.md)
  * [네트워크 네임스페이스간 ping통신](./network_namespace/Readme.md)
  * [네트워크 네임스페이스↔브릿지 ping통신](./network_namespace_bridge/Readme.md)
  * [네트워크 네임스페이스↔외부 ping통신](./network_namespace_gateway/Readme.md)
* 쿠버네티스 예제
  * [파드안 컨테이너간 통신](./pod_namespace/Readme.md)