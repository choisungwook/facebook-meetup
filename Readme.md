# 개요
* facebook 쿠버네티스 meetup 발표에서 사용되는 예제
  * 발표날짜: 22.3.19

# 쿠버네티스 설치
* vagrant로 설치를 자동화 했습니다.
> vagrantfile은 KANS스터디에서 제공했습니다.
```sh
# 배포 >> 윈도우(25분 소요), 맥(15분 소요)
vagrant up

# 배포 확인
vagrant status

# Linux Router(k8s-rtr) 접속
vagrant ssh k8s-rtr

# 마스터노드 접속
vagrant ssh k8s-m

# (워커)노드 접속
vagrant ssh k8s-w0
vagrant ssh k8s-w1
vagrant ssh k8s-w2
```

# 예제 목차
* [네트워크 네임스페이스간 ping통신](./network_namespace/Readme.md)
* [네트워크 네임스페이스↔브릿지 ping통신](./network_namespace_bridge/Readme.md)
* [네트워크 네임스페이스↔외부 ping통신](./network_namespace_bridge/Readme.md)
