# 1. 개요
* 파드안 컨테이너간 통신 예제입니다.

# 2. 첫번째 예제
* netshoot에서 80번포트가 없는지 확인합니다.
## 2.1 예제 설치
```sh
kubectl apply -f only_netshoot.yaml
```

## 2.2 포트 확인
* netshoot컨테이너에서 80번 포트가 없는 것을 확인합니다.
```sh
kubectl exec -it same-namespace -c netshoot -- ss -ntlp
```

## 2.3 예제 삭제
```
kubectl delete -f only_netshoot.yaml
```

# 3. 두번째 예제
* netshoot에서 80번 포트가 오픈되어 있는지 확인합니다.
* netshoot에서 127.0.0.1:80으로 nginx서비스를 호출합니다.

## 3.1 예제 설치
```sh
kubectl apply -f pod.yaml
```

## 3.2 포트 확인
* netshoot컨테이너에서 80번 포트가 없는 것을 확인합니다.
```sh
kubectl exec -it same-namespace -c netshoot -- ss -ntlp
```

## 3.3 netshoot 컨테이너 -> nginx 컨테이너
* netshoot컨테이너에서 127.0.0.1:80으로 nginx서비스를 호출할 수 있습니다.
```sh
kubectl exec -it same-namespace -c netshoot -- curl 127.0.0.1:80
```

## 2.4 예제 삭제
```
kubectl delete -f pod.yaml
```