# 개요
* 파드안 컨테이너간 통신 예제입니다.

# 예제 설치
```sh
kubectl apply -f pod.yaml
```

# 컨테이너 통신
* netshoot컨테이너에서 80번 포트가 없는 것을 확인합니다.
```sh
kubectl exec -it same-namespace -c netshoot -- ss -ntlp
```

* netshoot컨테이너에서 127.0.0.1:80으로 nginx서비스를 호출할 수 있습니다.
```sh
kubectl exec -it same-namespace -c netshoot -- curl 127.0.0.1:80
```

# 예제 삭제
```
kubectl delete -f pod.yaml
```
