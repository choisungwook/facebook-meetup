* busybox컨테이너에서 127.0.0.1:80으로 nginx서비스를 호출할 수 있습니다.
```sh
kubectl exec -it same-namespace -c netshoot -- curl 127.0.0.1:80
```