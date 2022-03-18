# 1. 개요
* kubedns 서비스(coredns) 예제 입니다.

# 2. 첫번째 예제: coredns tcpdump
> 유투브 영상: https://youtu.be/3srdG7mnVfY
## 2.1 coredns 배포 확인
```sh
kubectl -n kube-system get po | grep dns
kubectl -n kube-system get svc | grep dns
```

## 2.2 coredns pod갯수 1개로 설정
* 디버깅을 편하게 하기 위해 coredns pod갯수를 조절
```sh
kubectl scale deployment -n kube-system coredns --replicas=1
```

## 2.3 디버깅 pod 배포
* netshoot pod 배포
```
kubectl apply -f dnsquery.yaml
```

## 2.4 coredns 패킷 확인
* coredns에 연결된 calice 인터페이스에 tcpdump
```sh
CoreDNSveth=$(calicoctl get workloadEndpoint -n kube-system | grep coredns | awk '{print $5}' | cut -d "/" -f 1)
tcpdump -i $CoreDNSveth -nn udp port 53
```

* netshoot pod에서 dns쿼리 수행
```sh
kubectl exec -it dns-query -- dig google.com
```

# 3. 두번째 예제 - 서비스 디스커버리
> 유투브 링크: https://youtu.be/Hma6rSit65A
## 3.1 예제 pod, serice 배포
```sh
kubectl apply -f coredns.yaml
```

## 3.2 pod를 도메인으로 접근
```sh
kubectl exec -it coredns-example -- curl <pod-ip>.default.pod.cluster.local
```

## 3.3 서비스를 도메인으로 접근
```sh
kubectl exec -it coredns-example -- curl coredns-example.default.svc.cluster.local
```
