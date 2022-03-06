* 같은 노드 pod간통신
> 상세 과정은 블로그를 참고하세요: https://malwareanalysis.tistory.com/256

```sh
# calice-server pod ip확인
kubectl get po -o wide
# client -> server ping
kubectl exec -it calice-client -- ping -c <calice-server ip>
```
